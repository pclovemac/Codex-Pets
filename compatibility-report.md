# 兼容性与验证报告

## 结论

两套小音项目已经生成、完成确定性组装、通过 Codex v2 结构验证并安装。最终图集均为 `1536×2288`、8 列×11 行、单元 `192×208`、RGBA、`spriteVersionNumber: 2`，验证结果均为 `ok: true`、`errors: []`、`warnings: []`。

本次构建有一项用户批准的兼容性降级：第 10 行末三个方向（292.5°、315°、337.5°）仍偏向屏幕右上，未严格呈现要求的屏幕左上。用户已明确要求取消第 10 行限制并继续创建，因此该问题作为已知警告保留，不再阻断安装。成品可运行，但不宣称严格通过 hatch-pet 的全部方向语义门槛。

## 环境

- Codex Desktop：`26.1021.31345`，build `21828`，prod，更新状态 `up_to_date`。
- Codex CLI：`0.164.0-alpha.11.1`。
- workspace runtime bundle：`26.1024.11018`。
- hatch-pet：本机已安装；使用 v2 8×11 合同和内置确定性脚本。
- ImageGen：用于基础角色与动画整行生成；完整原图输入首次被审核拒绝，后续使用可追溯的脸/皇冠与蕾丝袖局部裁图。

## 已通过

- 官方 9 行状态：`idle`、`running-right`、`running-left`、`waving`、`jumping`、`failed`、`waiting`、`running`、`review`。
- 16 个方向单元均存在，尺寸、基线、透明通道和单元占用通过。
- 最终图集无空白必需单元、无跨单元边缘溢出、无透明 RGB 残留。
- 单次色键去边完成；结构校验 0 错误、0 警告。
- 联系表、方向预览、盲测题面、连续性报告和逐行动画 GIF 均保留在各自 `qa/` 目录。
- Chibi 连续性报告有 3 条人工复核提示；Original 有 1 条人工复核提示，均无 alpha 空洞，且不影响 v2 结构验证。

## 用户豁免与限制

- 豁免范围仅限第 10 行方向语义。
- 未豁免：8×11 结构、单元占用、裁切/串格、透明通道、色键去边、角色身份与整体风格一致性。
- `qa/user-direction-waiver.json` 保存用户指令及豁免范围。
- `qa/direction-semantics.json` 如实标注 292.5°、315°、337.5° 为 `waived_warning`。
- 因用户取消该限制，严格的三人方向盲测共识不作为本次安装门槛；盲测题面与答案键仍已生成供后续复核。

## 安装

- Chibi：`%USERPROFILE%\.codex\pets\xiaoyin-astra-chibi\`
- Original：`%USERPROFILE%\.codex\pets\xiaoyin-astra-original\`
- 每个安装目录只包含独立的 `pet.json` 与 `spritesheet.webp`。
- 安装前两个目录均不存在；没有覆盖现有宠物，也没有修改无关 Codex 配置。

在 Codex 宠物选择界面选择“**小音 · Astra Chibi**”或“**小音 · Astra Original**”即可切换。如列表没有立即刷新，请重启 Codex 桌面应用。
