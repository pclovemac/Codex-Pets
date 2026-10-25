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
