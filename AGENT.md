# AGENT.md

面向在本仓库工作的 AI 助手与维护者，记录**图标统一化处理流程**、**FlClash 适配原则**及配套约定。
改动 `Icons/`、`Script/`、`Config/` 里的内容前请先读本文。约定灵感源自 AIsouler/MyClash 的 AGENT.md。

## 0. 快速索引

| 项             | 位置 / 规则                                                                                                                                               |
| -------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 统一化矢量图标 | `Icons/svg/<Name>.svg`（共 38 枚）                                                                                                                        |
| 命名           | PascalCase、无下划线/连字符；与脚本/配置引用一一对应                                                                                                      |
| 图标引用格式   | `https://fastly.jsdelivr.net/gh/JokerXiaoMo/FlClash-Tuned@main/Icons/svg/<Name>.svg`；脚本里前缀为 `iconBaseUrl`；YAML 无变量，写全量                     |
| 规则集引用     | 脚本里前缀为 `ruleSetBaseUrl` → `https://fastly.jsdelivr.net/gh/MetaCubeX/meta-rules-dat@meta/geo/`；Emby 专属规则（emos/emby）为第三方仓库，仍写全量 URL |
| 回归测试       | `node Test/run-tests.js`（当前 182 项；改脚本必跑；含 ES2020 语法检查与 QuickJS 实跑 main()）                                                             |

## 1. 图标规范（Icons/svg/）

### 1.1 骨架与几何映射

```xml
<svg xmlns="http://www.w3.org/2000/svg" width="1024" height="1024" viewBox="0 0 1024 1024">
  <g transform="translate(tx ty) scale(s)">
    ...原始内容（坐标保持原样）...
  </g>
</svg>
```

- `s = 1024 / max(W, H)`，`tx = (1024 - W*s) / 2`，`ty = (1024 - H*s) / 2`（W/H 为原 viewBox 尺寸）。
- 效果：内容最长边正好 1024，另一方向等比居中留白（非 1:1 图标不拉伸铺满）。
- 底座（thesvg.org）不改形状，只做画布归一化；原创图标直接在 1024 画布上绘制。

### 1.2 二创与版权

- 底座来自 thesvg.org，仅选用 CC0-1.0 / MIT / Apache-2.0 许可的图标；禁止使用 CC-BY-ND（不可演绎）类底座。
- 每枚图标的来源与许可证登记在 `Icons/README.md`，新增/替换图标必须同步更新该表。

## 2. FlClash 适配原则（重要）

1. **不做端口/TUN/外部控制器设置**：`mixed-port`、`allow-lan`、`tun`、`external-controller`、`ntp` 等由 FlClash App 设置统一管理，脚本/配置中不得设置（否则与 App 补丁冲突）。
2. **规则集一律走 MetaCubeX meta-rules-dat**（FlClash 官方同源），不使用 Bettbox/bett-rules 系列来源。
3. **DNS 处理保留脚本逻辑**：使用本套件时需关闭 FlClash 的「DNS 覆写」开关，否则 App 补丁会覆盖脚本生成的 DNS 配置（README 中已说明）。
4. 移除所有 Bettbox 图形化适配代码（`Compatible_With_Bettbox` 等），不得回退。

## 3. 测试

```bash
node Test/run-tests.js            # 全部（含可选的 ES2020 / QuickJS 检查）
node Test/run-tests.js --node     # 仅 Node 单元+集成测试
```

- 脚本列表单一来源：`Test/lib/scripts.js`。
- 修改分流逻辑后必须跑 `node Test/run-tests.js` 全绿才能提交。
