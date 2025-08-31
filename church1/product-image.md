# Final Prompts: "Magical Drawing" Concept

This file contains the final, optimized prompts for generating the start/end frames and the video sequence for the "magical drawing" concept.

---

### 1. First Frame Prompt (for Text-to-Image)
_Use this prompt to generate the starting image of the blank paper._

**Prompt:**
`An extreme top-down shot of an empty, pristine sheet of high-quality watercolor paper in landscape orientation, centered on a rustic wooden desk. The scene is in a warm, quiet study, bathed in soft, diffuse, even light with golden hour tones, creating a bright atmosphere with minimal shadows and high contrast. The entire image is rendered in a retro watercolor hand-drawn style, with the paper's rich texture clearly visible and the surrounding desk softly blurred with creamy bokeh from an 85mm prime lens. The atmosphere is serene and full of potential.`

**中文释义:**
一张极致的俯拍照片：一张空白、崭新的高品质水彩画纸（横向放置）位于一张质朴的木制书桌中央。场景是一个温暖、安静的书房，沐浴在柔和、均匀的漫射光中，带有黄金时刻的色调，营造出明亮、阴影极少且高对比度的氛围。整个图像呈现为复古水彩手绘风格，画纸丰富的纹理清晰可见，周围的书桌则被85mm定焦镜头拍出柔和奶油般的虚化效果。整体氛围宁静，充满潜力。

---

### 2. Image Modification Prompt (for Image-to-Image)
_Use the image from prompt #1 as input, and apply this prompt to draw the chapel._

**Prompt:**
`On the watercolor paper, draw a beautifully detailed architectural illustration of a small, elegant medieval Catholic chapel. The mood should now feel one of accomplishment and timeless beauty.`

**中文释义:**
在水彩画纸上，绘制一幅精美、细节丰富的优雅中世纪天主教堂建筑插画。画面氛围应转变为一种充满成就感与永恒之美的感觉。

---

### 3. Video Generation Prompt (for Image-to-Video)
_Use the image from prompt #1 as the starting frame, and apply this prompt to animate the drawing process._

**Prompt:**
`Top-down, locked-off macro shot on watercolor paper (paper fills the frame, edges not visible). Lines of a medieval Catholic chapel appear and connect themselves; watercolor blooms spread organically to complete the illustration.`

**中文释义:**
俯拍、锁定的微距镜头，对准水彩纸（纸张填满画面，边缘不可见）。中世纪天主教堂的线条浮现并自行连接；水彩颜料有机地绽放开来，完成整幅插画。

---

### 4. Recommended Negative Prompt & Parameters
_Use these for all generations to ensure consistency and avoid unwanted elements._

**Negative Prompt:**
`hand, hands, human, person, arm, wrist, sleeve, glove, hand shadow, paintbrush, brush, pencil, pen, marker, stylus, palette, ruler, compass, eraser, water cup, easel, desk, table edge, foreground object`

**Parameters:**
`--ar 16:9`