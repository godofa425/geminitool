### 元提示 (Meta Prompt) V2: 2D插画转3D微缩景观视频 (段落式融合版)

**目标:** 创建一个简洁、有力、一气呵成的段落式英文Prompt。这个Prompt应该像一个导演的镜头脚本，将**核心动画**、**镜头运动**和**视觉风格**无缝地融合在一起，以指导AI模型生成一个将2D插画转变为3D微缩景观的视频。

**核心理念:** “一个镜头，一个故事”。我们不给AI零散的指令，而是给它一个完整的、动态的视觉叙事。

---

### Prompt 构建思路 (三步融合法)

在构思时，我们可以按以下三个核心要素来思考，但在最终输出时，必须将它们**融合进一个或两个段落中**，而不是分点罗列。

**1. 核心动画 (The Core Action):**
*   **思考:** 2D到3D的转变过程具体是怎样的？是缓慢生长，还是快速翻转？它的物理逻辑是什么？
*   **关键词:** 使用强有力的、具体的动词来描述。
    *   *好的例子 (我们成功的案例):* `pivoting on its bottom edge, the illustration flips up... slams down onto the surface... and upon impact, instantly snaps into its 3D form.` (以底部为轴翻起... 拍向表面... 撞击瞬间定格成3D形态。)
    *   *要避免的例子:* `magically transforms`, `grows into 3D`.
*   **细节:** 确保动画的逻辑是清晰的。比如，明确指出“纸张本身保持静止”。

**2. 镜头与场景 (The Camera & Scene):**
*   **思考:** 摄像机如何配合核心动画？它是在一旁静静观察，还是跟随动作运动？
*   **融合技巧:** 将镜头的动作和核心动画的动作写在**同一个句子里**，让它们同步发生。
    *   *好的例子 (我们成功的案例):* `As this happens [the church transforms], the camera circles the action, ending on a medium shot.` (当这一切发生时[教堂转变]，摄像机环绕着这个动作，最终停在中景。)
*   **场景元素:** 描述光照、背景和能增强氛围的关键元素。
    *   *关键词:* `soft directional window light`, `rustic wooden tabletop`.

**3. 视觉风格与质感 (The Aesthetic & Feel):**
*   **思考:** 最终画面的整体感觉是怎样的？要保留什么艺术风格？用什么效果来增强氛围？
*   **关键指令:**
    *   艺术风格: `The entire model must strictly retain its ink-and-watercolor aesthetic.`
    *   微缩感: `a shallow depth of field with a tilt-shift effect enhances the miniature feel.`
*   **融合技巧:** 这些指令可以作为独立的句子，放在核心动作描述之后，作为对整个场景的“渲染要求”。

---

### 最终输出格式示例 (我们成功的案例)

*   **输入图像:** 一幅水彩画，描绘了一个质朴的石头教堂。

*   **生成的Prompt (融合后的段落式):**
    > A cinematic video in a 9:16 vertical aspect ratio. The camera performs a slow orbit, starting with a top-down view of a finished ink-and-watercolor illustration of a small stone church on a sheet of paper, resting on a rustic wooden tabletop. Then, in a dynamic, forceful animation, the 2D church illustration, pivoting on its bottom edge, quickly flips up from the paper like a rigid cutout (the paper itself remains flat and stationary). It immediately slams back down onto the surface, and upon impact, it instantly snaps into its final, solid 3D diorama form. As this happens, the camera circles the action, ending on a medium shot. The entire model must strictly retain its ink-and-watercolor aesthetic. The scene is lit by soft, directional window light, and a shallow depth of field with a tilt-shift effect enhances the miniature feel.
    >
    > Once built, the church's small wooden doors open and a tiny, stylized person walks out.
    >
    > Sounds: A sharp whoosh as it flips up and a solid 'thud' as it lands, followed by a gentle acoustic piano score. A faint door creak, and a single distant church bell at the end.
