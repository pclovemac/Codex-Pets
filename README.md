# 小音 Codex 自定义桌面宠物

> 当前状态：两套 Codex v2 宠物均已生成、通过结构验证并安装。用户已明确取消第 10 行方向语义限制；因此成品可用，但不宣称严格通过 hatch-pet 的全部方向语义门槛。详见 `compatibility-report.md`。

本项目包含两个彼此独立的 Codex v2 宠物运行目录：

- `output/xiaoyin-astra-chibi/`：三头身 Q 版，安装 ID 为 `xiaoyin-astra-chibi`。
- `output/xiaoyin-astra-original/`：高保真原图风格版，安装 ID 为 `xiaoyin-astra-original`。

统一角色设定见 `character-spec.md`。参考图会被复制到各运行目录的 `references/reference-01.png`，生成提示、选择记录、确定性校验、预览和最终成品均保留在相应目录内。

## 本机兼容性基线

- Codex 桌面版：`26.1021.31345`，build `21828`，`prod` 渠道；更新检查结果为 `up_to_date`。
- Codex CLI：`0.164.0-alpha.11.1`。
- hatch-pet 合同：`spriteVersionNumber: 2`，8 列 × 11 行，单元 `192×208`，最终图集 `1536×2288`。
- 官方动画行：`idle`、`running-right`、`running-left`、`waving`、`jumping`、`failed`、`waiting`、`running`、`review`，另加 16 个顺时针注视方向。
- Python/Pillow：使用 Codex 内置 workspace runtime，不依赖系统 Python。
- 构建方式：内置 ImageGen 负责视觉生成；hatch-pet 脚本负责提取、统一缩放/基线、透明通道、图集组装、校验与预览。

## 提示词 - 根据自己需求修改

```
请使用我提供的参考人物图片，根据以下宠物角色设定制作一个完整的 Codex 自定义桌面宠物项目。


中文名称：小音
角色定位：优雅、可靠、温柔的私人 AI 秘书。

【原图识别】
先读取参考图片，分析人物的脸部轮廓、银白长发、刘海、水晶皇冠、眼睛、白色花瓣领口、蓝色蝴蝶结、蕾丝袖、刺绣以及整体3D CG幻想风格。原图为最终视觉身份基准，不允许生成与原角色无关的新人物。

【双版本设计】
A. Astra Chibi：3头身 Q版秘书宠物，保留原图身份特征，简化细节与服装结构，优先适配 Codex 小尺寸显示。
B. Astra Original：尽可能保留原图的3D CG人物比例、面容、服装、材质及优雅气质，制作适合动画的高保真版本。
两个版本使用独立目录，禁止互相覆盖，并且都要确保脸部、发色、皇冠及服装识别特征一致。

【配色】
雪白 #F5F3F1
银灰 #D8DDE7
冰蓝 #9BB9D7
深蓝 #293B63
水晶蓝 #B7DCE8

【动作设计】
待机：眨眼、呼吸、头发轻摆。
工作：手持文件板或操作电子面板。
思考：歪头、微皱眉、思考光点。
等待输入：抬头注视、双手托文件。
完成：微笑、点头、显示勾选。
错误：短暂困惑、警告提示。
休息：闭眼打盹。
欢迎：轻挥手、优雅鞠躬。
庆祝：轻盈旋转、少量雪花星光。

注意：上述是创意动作，不代表 Codex 官方状态。先检查已安装的 hatch-pet Skill 和当前 Codex 版本，读取准确的状态、资源规格与配置格式，映射官方支持的状态。对无法原生触发的附加动作，只保留为可扩展资源并说明限制。

【技术规范】
1. 先检查环境、技能与参考图片是否可以正常读取。
2. 检查官方宠物构建工作流，不要凭空假设配置字段或命令。
3. 先建立主角色设定与统一资产规范。
4. 分别生成 Q版和原图版视觉素材。
5. 生成符合实际 Skill 要求的动画、Spritesheet 和配置文件。
6. 统一画布尺寸、缩放、角色基准线与透明通道。
7. 检测每帧的角色一致性、裁切、重叠、循环跳帧与透明背景。
8. 保留源素材、预览图、可用成品及生成记录。
9. 先在独立输出目录验证，验证成功后再安装。
10. 不覆盖用户现有宠物、不修改无关配置。需要覆盖时先获得确认。

【交付】
- Q版宠物完整资源
- 原图风格宠物完整资源
- 各状态动画预览
- 角色设定表
- 兼容性检查结果
- 安装位置及启动方式
- 两个版本之间的切换说明

【执行策略】
首先完成环境检查与角色设计方案，然后按照当前环境所支持的能力尽可能执行生成、验证与安装。若缺少绘图工具、动画能力、Skill 或必要依赖，请明确指出缺失内容，不要虚构已生成的文件或成功安装的状态。
```

## 状态限制

Codex 原生只会触发上述官方状态。项目把欢迎映射到 `waving`，庆祝动势映射到 `jumping`，错误映射到 `failed`，等待输入映射到 `waiting`，工作/思考映射到 `running`，完成/复核映射到 `review`。独立的完整“思考、休息、庆祝、完成勾选”不能由当前原生状态机单独触发，因此只允许作为 `extensions/` 扩展素材存在，不会写入官方图集或 `pet.json`。

## 安装与切换

两个版本已分别安装到：

- `%USERPROFILE%\.codex\pets\xiaoyin-astra-chibi\`
- `%USERPROFILE%\.codex\pets\xiaoyin-astra-original\`

每个安装目录只包含经校验的 `pet.json` 与 `spritesheet.webp`。两套 ID 和目录不同，不会互相覆盖。安装后在 Codex 的宠物选择界面选择“**小音 · Astra Chibi**”或“**小音 · Astra Original**”即可切换；如界面未即时刷新，重启 Codex 桌面应用后再选择。

## 验证门槛

本次安装保留以下硬性门槛：

1. 标准 9 行逐帧提取与连通性检查通过。
2. 16 个注视方向均有可用单元，连续性检查完成；第 10 行末三格的严格方向语义由用户明确豁免。
3. 最终透明图集尺寸、已用/未用单元、色键去边和 v2 格式校验通过。
4. 联系表、逐行动画 GIF 与方向预览完成视觉检查；方向偏差记录在 `qa/direction-semantics.json`。

构建完成后的权威结果记录在每个版本的 `qa/run-summary.json`。

## 仓库结构

- `dist/`：可直接安装的两个宠物包，每个目录只包含 `pet.json` 与 `spritesheet.webp`。
- `source/`：用户提供的参考图及用于保持角色身份的局部参考。
- `output/`：最终图集、生成提示、动画预览与 QA 报告。
- `extensions/`：当前 Codex 原生状态无法单独触发的创意动作说明。
- `character-spec.md`：统一角色身份、配色、服装与双版本规范。
- `compatibility-report.md`：环境、验证结果、已知限制与安装记录。
- `generation-log.md`：生成与确定性组装过程。

可再生成的逐帧文件、解码中间图、失败尝试和机器本地绝对路径清单通过 `.gitignore` 排除，但仍保留在本地工作目录中。

## 从仓库安装

将所需版本的整个目录复制到 `%USERPROFILE%\.codex\pets\`：

```powershell
Copy-Item -Recurse -LiteralPath '.\dist\xiaoyin-astra-chibi' -Destination "$env:USERPROFILE\.codex\pets\xiaoyin-astra-chibi"
```

如需原图比例版，将命令中的 `xiaoyin-astra-chibi` 替换为 `xiaoyin-astra-original`。若目标目录已经存在，请先自行备份；不要直接覆盖现有宠物。
