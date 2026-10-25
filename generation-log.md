# 小音生成记录

## 2026-10-25 环境与输入

- 原始参考图：`source/reference-original.png`（从用户提供路径复制，未修改）。
- 安全身份裁图：`source/identity-face-crown.png`，保留脸型、眼睛、银白长发、刘海、冰晶皇冠、高领与深蓝蝴蝶结。
- 安全材质裁图：`source/costume-lace-sleeve.png`，保留半透明蕾丝袖与花卉刺绣材质。
- Codex 桌面版：`26.1021.31345` / build `21828` / prod / up to date。
- Codex CLI：`0.164.0-alpha.11.1`。
- workspace runtime bundle：`26.1024.11018`，使用其内置 Python 与 Pillow。
- hatch-pet：本机已安装；使用 v2 8×11 合同。

## 输入审核处理

第一次直接附加完整参考图生成两个基础视觉时，内置 ImageGen 均在输入审核阶段拒绝，未产生任何图像或文件。为继续保持可追溯的视觉身份，同时排除与宠物制作无关的画面区域，后续生成只附加上述脸部/皇冠和蕾丝袖局部裁图；完整原图仍保存在 `source/reference-original.png`，不作为后续 ImageGen 输入。

## 目录隔离

- Chibi：`output/xiaoyin-astra-chibi/`
- Original：`output/xiaoyin-astra-original/`

两个目录拥有独立的 `pet_request.json`、`imagegen-jobs.json`、提示、解码资产、帧、QA、预览和最终图集，安装 ID 也不同。

## 2026-10-25 最终组装与安装

- 用户指令“取消第10行的限制然后创建”被记录为只豁免第 10 行方向语义，不豁免尺寸、透明通道、单元占用、边缘裁切和串格检查。
- Chibi 第 9 行原注册结果因相邻发丝连接导致两个稀疏单元；使用 hatch-pet 的等分槽提取方式从完整生成行重新提取，保留整行来源并修复串格。
- 两套方向行均采用整行来源做确定性等分槽提取，再统一缩放、基线、透明通道和一次性色键去边。
- 两套最终图集均通过 `validate_atlas.py --require-v2`：1536×2288、8×11、RGBA、`spriteVersionNumber: 2`、0 个错误、0 个警告。
- 第 10 行的 292.5°、315°、337.5°仍带屏幕右上偏差，已作为用户豁免警告保存在 `qa/direction-semantics.json`，因此不宣称严格方向语义合规。
- 安装时先确认两个目标目录均不存在；随后创建独立目录，没有覆盖现有宠物或修改无关配置。
