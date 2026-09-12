# Refresh Chart

参考图驱动的图表焕新技能：从现有 SVG 出发，经方案问答和英文效果预览，生成中文可编辑 SVG，并使用可选 CSV 核验数据。

An AI skill for refreshing SVG charts from visual references, with design Q&A, English previews, editable Chinese SVG output, and optional CSV-based data validation.

## 输入

| 材料 | 是否必需 | 用途 |
| --- | --- | --- |
| A：风格参考图 | 必需 | 配色、轮廓、填充与布局参考 |
| B：自己的 SVG 图表 | 必需 | 图表内容、变量、单位与功能 |
| C：CSV 数据，可多份 | 可选 | 精确重绘与数据核验 |

缺少 A 或 B 时，技能会先索取。当前版本不包含以图片替代 B 的数据重建流程；没有 CSV 时复用并核对原 SVG，不声称已核验原始数据。

## 工作流程

1. 分析原图的阅读任务，以及参考图的图形类型是否适用。
2. 推荐有实际价值的升级方案，明确必须保留的信息。
3. 在生成前进行 Q&A：选择具体方案，也可以自由填写建议。
4. 生成英文 AI 效果预览。
5. 根据 CSV 或原 SVG 的矢量信息精确重绘。
6. 中文排版、数据和渲染核验，交付可编辑 SVG、PNG 预览、核验记录和构建脚本。

用户选定方案后，默认连续完成；若明确要求“先到预览”，则停在预览。已有明确授权不会重复询问。

## 安装与调用

将本仓库克隆到 Codex 的技能目录（目标目录应不存在）：

```sh
git clone https://github.com/LawrenceRiver/refresh-chart.git "${CODEX_HOME:-$HOME/.codex}/skills/refresh-chart"
```

在能够发现该技能的 Codex 会话中，附上材料并调用：

```text
请使用 $refresh-chart。A 是风格参考图，B 是我的 SVG，C 是配套 CSV。
先评估是否适合改换图表类型，再让我选择方案，随后完成英文预览和中文可编辑 SVG。
```

## 环境与输出

- 需要能够读写本地 SVG/CSV、运行重绘脚本和渲染 SVG 的代理环境。
- 英文 AI 预览需要可用的图像生成工具；工具不可用时会说明，不冒充已生成。
- 中文字体：PingFang SC（苹方）。公式字体：STIX Two Math；变量数学斜体，数字、运算符和单位正体。字体不随仓库分发，缺失时需另行准备。
- 文字、曲线、填充、图例与坐标保持可编辑，不以整图位图冒充 SVG。
- AI 预览用于评估设计，精确数值由数据重绘保证。核验图表数据不代表证明底层模型或实验结论。

## 文件

- [SKILL.md](SKILL.md)：完整工作流程。
- [references/svg-and-data.md](references/svg-and-data.md)：矢量重绘与数据核验细节。
- [agents/openai.yaml](agents/openai.yaml)：技能界面元数据。

适用于时序图、柱状图、分布图等数据图表；不用于设备架构图或流程图。
