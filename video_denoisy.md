# ASMR视频音频优化手册

## 任务目标
对ASMR视频的音频轨进行优化处理，去除刺耳高频，增强低频温暖感，创造柔和舒缓的听感体验。

## 流程步骤

1. **备份原视频文件**
   ```bash
   cp input.mp4 input_backup.mp4
   ```

2. **提取音频**
   ```bash
   ffmpeg -i input.mp4 -vn -acodec pcm_s16le audio.wav
   ```

3. **分析音频特征**
   ```bash
   # 提取关键数值
   FULL_RMS=$(sox audio.wav -n stat 2>&1 | grep "RMS amplitude" | awk '{print $3}')
   HF_RMS=$(sox audio.wav -n highpass 6000 stat 2>&1 | grep "RMS amplitude" | awk '{print $3}')
   HF_RATIO=$(echo "scale=3; $HF_RMS / $FULL_RMS" | bc)
   echo "高频能量比: $HF_RATIO"
   ```

4. **ASMR音频处理**
   
   根据高频能量选择处理强度：

   **轻微噪声**（HF_ratio < 0.10）：
   ```bash
   ffmpeg -i audio.wav -af "\
   highshelf=f=8000:g=-1:t=q:w=1.0,\
   lowshelf=f=150:g=1.5:t=q:w=0.8,\
   acompressor=threshold=0.2:ratio=1.5:attack=40:release=200,\
   alimiter=limit=0.94,\
   volume=0.8" audio_fixed.wav
   ```

   **标准处理**（HF_ratio 0.10-0.20）：
   ```bash
   ffmpeg -i audio.wav -af "\
   highshelf=f=6000:g=-2:t=q:w=1.2,\
   highshelf=f=10000:g=-3:t=q:w=0.8,\
   lowshelf=f=200:g=1:t=q:w=0.7,\
   alimiter=limit=0.92,\
   volume=0.8" audio_fixed.wav
   ```
   
   *注：`volume=0.8` 将音量降低20%，如不需要可去除此参数*

   **保守处理**（HF_ratio > 0.20 或噪声严重）：
   ```bash
   ffmpeg -i audio.wav -af "\
   lowpass=f=6000:p=1,\
   highshelf=f=4000:g=-4:t=q:w=1.0,\
   lowshelf=f=120:g=3:t=q:w=0.9,\
   acompressor=threshold=0.05:ratio=3:attack=30:release=150,\
   alimiter=limit=0.88,\
   volume=0.8" audio_fixed.wav
   ```
   
   *注：`volume=0.8` 将音量降低20%，如不需要可去除此参数*

5. **合成最终视频**
   ```bash
   ffmpeg -i input.mp4 -i audio_fixed.wav -map 0:v:0 -map 1:a:0 -c:v copy -c:a aac -b:a 128k output_asmr.mp4
   ```

## 完整自动化脚本

```bash
#!/bin/bash
# ASMR视频音频优化脚本
# 使用方法: ./asmr_audio.sh input_video.mp4

INPUT_VIDEO="$1"
if [ -z "$INPUT_VIDEO" ]; then
    echo "Usage: $0 <input_video.mp4>"
    exit 1
fi

echo "=== ASMR音频优化处理 ==="

# 1. 工具检查
command -v ffmpeg >/dev/null 2>&1 || { echo "请先安装 ffmpeg"; exit 1; }
command -v sox >/dev/null 2>&1 || { echo "请先安装 sox"; exit 1; }
command -v bc >/dev/null 2>&1 || { echo "请先安装 bc"; exit 1; }

# 2. 备份和提取音频
echo "备份原视频..."
cp "$INPUT_VIDEO" "input_backup.mp4"
echo "提取音频..."
ffmpeg -i "$INPUT_VIDEO" -vn -acodec pcm_s16le audio.wav -y

# 3. 分析音频特征
echo "分析音频特征..."
FULL_RMS=$(sox audio.wav -n stat 2>&1 | grep "RMS amplitude" | awk '{print $3}')
HF_RMS=$(sox audio.wav -n highpass 6000 stat 2>&1 | grep "RMS amplitude" | awk '{print $3}')
HF_RATIO=$(echo "scale=3; $HF_RMS / $FULL_RMS" | bc)

echo "高频能量比: $HF_RATIO ($(echo "scale=1; $HF_RATIO * 100" | bc)%)"

# 4. 根据分析结果选择ASMR处理方案
# 音量调整设置（可选）
# VOLUME_ADJUST=",volume=0.8"  # 降低20%音量，取消注释以启用
VOLUME_ADJUST=""  # 默认不调整音量

if (( $(echo "$HF_RATIO > 0.20" | bc -l) )); then
    echo "应用保守ASMR处理（噪声较多）..."
    ffmpeg -i audio.wav -af "\
    lowpass=f=6000:p=1,\
    highshelf=f=4000:g=-4:t=q:w=1.0,\
    lowshelf=f=120:g=3:t=q:w=0.9,\
    acompressor=threshold=0.05:ratio=3:attack=30:release=150,\
    alimiter=limit=0.88$VOLUME_ADJUST" audio_fixed.wav -y
elif (( $(echo "$HF_RATIO > 0.10" | bc -l) )); then
    echo "应用标准ASMR处理..."
    ffmpeg -i audio.wav -af "\
    highshelf=f=6000:g=-2:t=q:w=1.2,\
    highshelf=f=10000:g=-3:t=q:w=0.8,\
    lowshelf=f=200:g=1:t=q:w=0.7,\
    alimiter=limit=0.92$VOLUME_ADJUST" audio_fixed.wav -y
else
    echo "应用轻微ASMR优化..."
    ffmpeg -i audio.wav -af "\
    highshelf=f=8000:g=-1:t=q:w=1.0,\
    lowshelf=f=150:g=1.5:t=q:w=0.8,\
    acompressor=threshold=0.2:ratio=1.5:attack=40:release=200,\
    alimiter=limit=0.94$VOLUME_ADJUST" audio_fixed.wav -y
fi

# 5. 合成最终视频
echo "合成最终视频..."
ffmpeg -i "$INPUT_VIDEO" -i audio_fixed.wav -map 0:v:0 -map 1:a:0 -c:v copy -c:a aac -b:a 128k output_asmr.mp4 -y

echo "=== 处理完成 ==="
echo "输出文件: output_asmr.mp4"
echo "备份文件: input_backup.mp4"
```

## ASMR处理参数说明

### 频率处理
- **高频衰减**：6000Hz (-2dB), 10000Hz (-3dB) - 去除刺耳成分
- **低频增强**：120-200Hz (+1-3dB) - 增加温暖感
- **低通滤波**：6000Hz截止（仅用于噪声严重情况）

### 动态处理
- **压缩比**：1.5:1 到 3:1 - 温和压缩
- **攻击时间**：30-40ms - 避免突兀
- **释放时间**：150-200ms - 保持自然
- **限幅**：88%-94% - 保守设置避免失真

### 音频码率
- **AAC 128k** - ASMR视频的理想码率，温和且节省空间

### 音量控制
- **volume=0.8** - 降低音量20%（0.8倍）
- **volume=0.6** - 降低音量40%（0.6倍）
- **volume=1.0** - 保持原音量（默认）
- **音量调整范围**：建议0.6-1.0之间，避免过度降低导致动态范围损失

## 依赖工具

安装命令：
```bash
brew install ffmpeg sox bc
```

## 使用建议

1. **测试环境**：使用耳机测试效果，因为ASMR主要通过耳机收听
2. **音量控制**：ASMR音频通常音量较低，可根据需要调整volume参数
   - 如果原音频过响，建议使用`volume=0.8`降低20%
   - 如果有突发尖锐声音，建议使用`volume=0.6-0.7`
3. **听感验证**：处理后进行A/B对比，确保达到舒缓效果
4. **保留备份**：始终保留原始文件以便对比和调整
5. **音量测试**：在不同设备上测试音量是否合适，避免过小或过大

## 质量检查清单

处理完成后，请检查：
- ✓ 声音是否柔和不刺耳
- ✓ 是否保留了温暖的低频感
- ✓ 没有明显的处理痕迹
- ✓ 整体听感是否舒缓放松
- ✓ 音量是否适中（不会突然惊扰听众）