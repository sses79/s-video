---
name: ksrmj
description: "KSR MJ prompt writing system for cinematic first-pass image generation on Neo MJ (Midjourney v8.1 mirror, Chinese direct input supported). Use when the user needs Midjourney/MJ prompts, Neo站出图, first-pass scene plates, posters, VFX, city establishing shots, or any MJ提示词编写 with 元启录-style one-paragraph five-section structure, practical-set anchors, mood recipe cards, and master DP references. Outputs Chinese direct-input + English dual versions. Pipeline 3.0 station one (MJ first pass → GPT stabilization). Character four-grid sheets go to KSRIM-人设 instead; GPT image stabilization goes to KSRIM-生图."
---

# KSRMJ — K系MJ提示词系统

## 定位

KSRMJ是产线3.0的第一站：用MJ（Neo站，v8.1，支持中文直输）出**第一版构图、光影、氛围骨架**。

产线3.0全链：
1. **MJ第一版**（本skill）：构图骨架+摄影美学，吃MJ「像摄影师一样理解光」的天花板
2. **GPT稳固**（KSRIM-生图 skill）：换元素、统一材质、清细碎细节，im2负面卫生管这段
3. **GRANDI降级可选**：锐化收尾，试参数不进片

**为什么这么走**：GPT直出的死板是模型级美学天花板，提示词治不了；MJ→GPT混合工作流是行业头部项目（元启录2工程文件）验证的路线。

## 技能分工

| 任务 | 技能 |
|---|---|
| 场景/海报/VFX第一版出图 | **KSRMJ**（本skill） |
| GPT稳固/改图/局部重画/统一材质 | KSRIM-生图 |
| 角色四宫格人设 | KSRIM-人设（不走MJ） |

## 第零步：Creative Meeting前置三问（v2）

写五段论之前先答三问——prompt是摄影师工作笔记（Photographer's Notes），不是物体清单（Object List）：

1. **这一幕真正拍的是什么？** 情绪主题（孤独/等待/回忆/对峙/敬畏……）——不是「有什么」，是「为什么拍」
2. **哪个Moment？** 「刚刚发生了什么」：她刚停下脚步＞她站着；箭没射出＞箭射出——Anticipation is stronger than Action
3. **克制什么？** 电影感来自决定「不拍什么」：不拍天空/不强调英雄感/保持安静

三问对接五段论：Q1定情绪配方卡，Q2定第三段主体动作句式（「刚刚」式），Q3定负空间配额+克制度句式。完整句式库（Story Moment/Attention指向表/Visual Hook三眼序列）见 `references/cinematic-thinking.md`。

---

## 一段式五段论（默认模板）

所有KSRMJ提示词按此顺序写成**一段连续长文**（不打分点，MJ吃一段式）：

1. **类型声明**：第一句定生死
2. **构图机位**：机位物理指纹（高度+角度+光学+构图规则+前景层+负空间）
3. **主体与环境**：逐人锚定+占比控制+环境材质清单
4. **光与材质**：光方向/质量/时辰+调色板+实拍锚系统+情绪配方注入
5. **负向+参数**：负向组合拳+参数行

---

## 第一段：类型声明（第一句定生死）

第一句必须包含：**媒介真实性声明+类型+画幅**。

中文模板：
- 场景：「一张真实电影摄影质感的史诗奇幻[XX]场景，21:9超宽银幕构图」
- 街景空镜：「一张真实电影摄影质感的奇幻蒸汽朋克城市街道闹市场景，21:9超宽银幕构图」
- 建筑：「极致写实的建筑摄影，一座[形容词堆]的[XX]建筑」
- 角色剧照：「一张纯真人实拍质感的电影角色定妆半身照」（常规人设走KSRIM-人设，仅电影级单人剧照用MJ）
- 特效：「一张真人电影级[XX]特效画面，竖版构图」

英文模板：
- 「Photoreal live-action [XX] scene, 21:9 wide frame.」
- 「Photoreal live-action fantasy harbor at deep night, low-key exposure.」
- 「Photoreal feature-film VFX plate on a clean solid medium-gray seamless background.」
- 「Live-action prestige fantasy poster, 3:4 vertical, only two characters.」

## 第二段：构图机位（物理指纹）

用**物理事实**写机位，不用形容词。写只有该机位才成立的物理事实：

- 高度+角度写死：「镜头位于半空中航拍微俯视角，中远景构图」/「Camera near the ceiling, side 45-degree downward wide-angle view」/「wide 28mm lens at pedestrian height」/「wide eye-level view」
- **大型建筑鸟瞰锚（直接抄母版）**：「极高空高机位俯视鸟瞰，大远景景别，专业无人机航拍，24毫米全画幅超广角镜头，镜头位于[建筑]最高尖塔上方数百米的高空，摄影机高度远远高于[建筑]所有穹顶与尖塔，摄影机以约60度角明显向下倾斜拍摄，画面中能够清晰看到大量[屋顶清单]之间的完整空间关系；地面和屋顶占据画面大部分面积，地平线位于画面最上方或完全不可见」
- 光学：24mm全画幅超广角 / wide 28mm / 35mm / 85mm portrait lens / 变形宽银幕镜头 anamorphic
- 构图规则（选1-2，点名）：三分法 / 双侧对称 / 单点透视灭点 / 引导线 / 框中框 / 负空间 / 对角线 / 非对称对角布局
- 前景层：写一个具体前景元素（雾/栏杆/玻璃/残垣/拱门）——没有前景层的画面读起来平
- 负空间配额：30-50%画面刻意留空（天空/雾/墙/阴影/水面）

## 第三段：主体与环境

- **多人场景=逐人锚定**（防撞脸防同装）：每人写死脸型/发色/服装/武器，武器各异。中文「1号：…；2号：…；3号：…」；英文「distinct men: left [脸+发+武器]; center […]; right […]」
- **占比控制**（防主体撑爆画面）：「龙不要特别巨大，不要占满天空」「城市在画面中的占比保持克制，不要放大，不要贴近镜头」「大炮不要占满画面」「天空占据画面很大比例」
- **克制度句式**（防MJ美学过度）：「服装精致但不过度夸张」「克制、精密、真实，不要过度科幻，不要赛博朋克」「restrained brass pipes and sparse dim amber lanterns」
- 环境清单：逐物写实（「泥地、草丛、帐篷、木栅栏、战旗、火盆」+「地面有泥水、脚印、车辙和真实湿润反光」）
- **画面内不要出现可读文字**：正文预埋「画面中不要出现任何可读文字」

## 第四段：光与材质（实拍锚系统+K系注入）

### 实拍锚系统（防CG感灵魂——每条必挂，四类至少挂三）

1. **相机锚**：ARRI Alexa Mini LF（最高频）/ ARRI Alexa look / Sony A7R IV（人像向）
2. **镜头胶片锚**：24mm/28mm/35mm/85mm portrait lens、35mm film look、Fuji 400H film color、Kodak 65mm、subtle film grain、变形宽银幕镜头
3. **现场证据链**：practical set realism、real actors、practical prosthetics、real extras、real costumes、on-location film still、「像真实电影里的高级服装和实物特效妆造」
4. **物理光照**：光由画面内实际光源驱动（烛台/壁炉/灯笼/月光/火盆），电影级布光、真实阴影

材质清单模式：「真实摄影感，真实[材质1]、真实[材质2]、真实[材质3]……」——每个环境物配一个真实材质词。

### 情绪配方卡（K系注入，详见 references/mood-master-injection.md）

情绪通过物理落地。**最多1个氛围词当调味，禁抽象情绪词堆叠**。八张速查：

```text
epic        → 超远景/低角度/留白过半/黄昏或单色冷调/变形宽银幕
solitary    → 全景/负空间/降饱和/剪影或背影
danger      → 低调布光/单硬侧光源/深阴影/冷调/紧框架
unease      → 斜角/高对比/压迫式构图
poetic      → 中景全景/侧角度/柔光/邻近色/胶片颗粒
sacred      → 体积光/顶光/对称
gritty real → 阴天自然光/降饱和/16mm颗粒感/手持感
intimate    → 浅景深/近景尺度/柔光/暖点缀
```

### 大师参考层（K系注入，辅助）

以**设备/胶片锚为主**（MJ响应稳），DP参考一句为辅（≤2）：雾→Deakins Sicario；沙漠/巨物→Fraser Dune；霓虹→Doyle花样年华；烛光→Willis教父；对称→Yeoman布达佩斯；色块→张艺谋英雄；冷写实→Hoytema敦刻尔克。

### K系禁词（继承KSRIM-生图）

- 禁8K/ultra detailed/超高清画质吹水——保持材质物理+胶片锚（元启录城堡版带过8K，K系不带）
- 禁运镜词（dolly/pan/tracking/crane）——静态图只写运动痕迹（motion blur）
- 氛围词≤1个

## 第五段：负向组合拳+参数

### 负向组合拳（四拳制，总量8-14词）

1. **风格拳**（必挂）：不要CG感、不要3D渲染、不要游戏截图、不要插画感、不要动漫、不要塑料材质
2. **时代拳**（按世界观配）：不要现代汽车/现代广告牌/霓虹灯/摩天楼/现代坦克/现代火炮/投石车
3. **水印拳**（必挂）：不要文字、不要字母、不要标识、不要Logo、不要水印
4. **场景死亡点**（按类型预埋，每类3-5个）：
   - 夜景：不要强光（no bright light）
   - 战争天空：不要明亮天空、不要薄云
   - 水系VFX：不要卡通水花、不要插画线条
   - 森林：不要前景溪流（不需要时）
   - 城市远景：不要活龙（石雕世界观）、不要积雪（按季节）
   - 群像：不要额外人物、不要相似脸、不要背面（需正面时）

**负向纪律**（K系原则）：负向是广谱失效类预埋，**不是旧失败记忆**。禁把旧项目失败的具体物件写进负向。

### 参数矩阵

| 类型 | 参数 |
|---|---|
| 场景/空镜 | `--ar 21:9 --style raw --preview` |
| 常规场景（人群/森林） | `--v 8.1 --raw --s 100 --hd --preview` + `--no [英文连写]` |
| 海报竖版 | `--ar 3:4`（或 2:3 / 9:16）`--style raw --preview` |
| VFX高可控 | `--v 8.1 --raw --s 35 --chaos 0 --hd --preview` |
| VFX高美学 | `--s 70`；变异探索 `--s 150 --chaos 0` |

中文直输时参数行用英文原样；中文版负向写句尾「完全不要XX、不要XX」，或合并进 `--no` 英文连写。

## 双版本输出规则

每个画面输出两版，K哥现场择优：
1. **中文直输版**：Neo站支持中文直接输入。复杂场景母版（建筑群/多人/长环境清单）优先中文长版——信息量大，中文处理不弱
2. **英文版**：标准MJ语法。海报/VFX/标准场景优先英文短版——美学响应更稳

## 批量抽卡工作流

1. **判断类型**：场景/海报/VFX（人设→转KSRIM-人设）
2. **构图骨架先行**：hero资产先把景别/机位物理/光学/构图规则/前景/负空间3-5个关键词给K哥签字，再写全文
3. 选情绪配方卡1张+大师DP锚（≤2）
4. 填五段论模板（读 references/yq2-patterns.md 拿对应母版改）
5. 挂实拍锚+负向拳+参数
6. 输出双版本
7. **抽卡**：同底座微调3-4版批量跑（城堡×3微调/海报×10迭代是元启录验证的节奏）。无神提示词，只有好底座+批量迭代
8. 出图验收：对照预埋fail-points清单逐项过（结构>构图>材质），硬点失败重抽不修补
9. 底图满意→转GPT稳固（KSRIM-生图）：换元素/统一材质/清细节

## 永恒黄昏适配模块（按需挂载）

- 银镜城/底层夜晚：**100%冷色零暖色**（唯一例外=教廷老金点缀）
- 夜晚基调：深蓝灰/藏蓝夜空/冷暗蓝灰，禁暖光污染；黄昏=暗橙天
- 术语：「帝国」禁用→「永暮教廷/Clergy」；6区>7区（阶层上优下劣）
- 银镜城鸟瞰：直接抄城堡鸟瞰母版，色温替换（冷银月光→黄昏暗橙天/银灰金属/教廷老金点缀）

## References

- `references/yq2-patterns.md`：元启录2工程逆向资产库——五段论母版逐条解剖、句子级可抄清单、参数矩阵原始出处
- `references/mood-master-injection.md`：K系注入层完整版——情绪配方卡八张+大师参考层十组DP匹配表+注入写法

## Changelog

- v2 (0829)：增量吸收cinematic-director体系思考前置层——新增第零步Creative Meeting三问+references/cinematic-thinking.md（Story Moment句式库/Attention指向表/Visual Hook三眼序列/核心思想四条）。原五段论/实拍锚/负向拳/参数矩阵零改动。
- v1 (0829)：初版。骨架=元启录2工程逆向（一段式五段论/实拍锚系统/负向组合拳/克制度句式/占比控制/参数矩阵/批量抽卡）；注入=K系三层（构图逻辑/情绪配方卡/大师参考层）。来源：元启录2工程30+条提示词逆向 + im2 v6融合 + 情报验证（GPT死板=模型级现象，MJ→GPT混合工作流行业头部通行）
