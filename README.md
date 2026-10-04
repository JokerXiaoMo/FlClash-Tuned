# FlClash-Tuned

<div align="center">

**为 [FlClash](https://github.com/chen08209/FlClash) 完全深度适配的 mihomo 覆写特调套件**

基于 [AIsouler/MyClash](https://github.com/AIsouler/MyClash) 的特调思路重构：剔除 Bettbox 图形化适配，全面转向 FlClash 生态

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Tests](https://img.shields.io/badge/Tests-182%20passed-brightgreen)](Test)
[![Icons](https://img.shields.io/badge/Icons-%E7%B0%AA%E8%8A%B1%E5%8D%B0%2040%20SVG-E58BA8)](Icons)

</div>

## 这是什么

MyClash 是面向 Bettbox 深度适配的 mihomo 覆写脚本与配置文件项目。本项目继承其全部特调功力，并做以下深度改造：

| 维度 | MyClash（原版） | FlClash-Tuned（本项目） |
| ---- | --------------- | ----------------------- |
| 目标客户端 | Bettbox | **FlClash** |
| 图形化适配 | Bettbox 参数桥接 | 移除；适配 FlClash 覆写体系 |
| 规则集来源 | appshubcc/bett-rules | **MetaCubeX meta-rules-dat**（FlClash 官方同源） |
| 端口/TUN/控制器 | 脚本内写死 | 交由 FlClash App 设置管理，互不冲突 |
| 图标 | 原版图标 | **「簪花印」全套 40 枚 1024×1024 SVG**（桃粉底白符，来自 [taobai-zanhua](https://github.com/JokerXiaoMo/taobai-zanhua) 姐妹项目） |
| 测试 | 192 项 | 182 项全绿（随功能演进） |

## 特色功能

- 🧩 **22 个分流策略组**：AI、YouTube、Google、Telegram、Steam、Netflix、Spotify、TikTok、Meta、Line、Microsoft、Apple、Emby、PikPak、PayPal、Patreon、EHentai、Crypto、FCM、AdBlock 等，可逐个开关
- 🌏 **地区节点自动分组**：自动识别香港/日本/美国/新加坡/台湾省并生成策略组（含自动测速组与倍率组）
- 🧹 **节点智能整理**：自动补国旗、规范化命名、过滤无效节点、按倍率分类
- 🛡️ **无 DNS 泄露**：DNS 与路由规则配套设计，自动处理机场私有 DNS 与节点域名 hosts 映射
- 🪶 **轻量规则集**：rule-provider 按需加载（.mrs），全部来自 MetaCubeX
- 🎨 **簪花印图标**：40 枚统一 1024×1024 的 SVG，桃粉底白符，FlClash 任意主题下都清晰
- 🪜 **高级代理**：自定义节点、链式代理、IPv4/IPv6 优先、屏蔽国外 QUIC

## 快速开始（覆写脚本）

> 前提：FlClash 已导入机场订阅。脚本仅用于覆写机场配置，请勿用于覆写自行编写的完整配置。

1. 打开 FlClash → **配置** → 点击订阅 → **编辑** → **覆写** → 添加 **脚本** 类型
2. 粘贴对应链接（二选一）：

| 版本 | 链接 |
| ---- | ---- |
| **全量版**（22 个分流组） | `https://raw.githubusercontent.com/JokerXiaoMo/FlClash-Tuned/main/Script/flclashScript.js` |
| **精简版**（常用分流组） | `https://raw.githubusercontent.com/JokerXiaoMo/FlClash-Tuned/main/Script/flclashScriptLite.js` |

3. **关闭 FlClash 的「DNS 覆写」开关**（设置 → DNS 覆写 关），确保脚本的无泄露 DNS 逻辑生效
4. 保存后回到首页，重新连接即可看到分组与图标

> 💡 也可直接复制脚本全文粘贴到覆写脚本编辑器中。

## 静态配置（可选）

若不想用覆写脚本，可直接导入静态配置（注意静态版无法动态识别地区节点）：

| 版本 | 链接 |
| ---- | ---- |
| 全量版 | `https://raw.githubusercontent.com/JokerXiaoMo/FlClash-Tuned/main/Config/flclashConfig.yaml` |
| 精简版 | `https://raw.githubusercontent.com/JokerXiaoMo/FlClash-Tuned/main/Config/flclashConfigLite.yaml` |

FlClash 导入方式：首页 → 配置 → 添加配置 → 从 URL 导入（也支持 `clashmeta://` / `flclash://` 链接唤起）。

## 可配置选项

脚本顶部 `ruleOptionsEnable` 即全部开关：22 个分流组开关，以及：

| 选项 | 说明 | 默认 |
| ---- | ---- | ---- |
| 极简模式 | 只保留「默认代理」 | 关 |
| 生成地区自动选择组 | 每地区附带 URLTest 自动组 | 开 |
| 隐藏地区手动选择组 | 隐藏手动选择地区组 | 关 |
| 生成倍率组 | 低/高倍率节点分组 | 开 |
| 分流组添加所有节点 | 分流组列出全部节点 | 关 |
| 过滤低/高倍率节点 | 剔除对应倍率节点 | 关 |
| 过滤非地区节点 | 剔除公告/官网类节点 | 开 |
| 屏蔽国外QUIC | 阻断境外 QUIC 流量 | 开 |
| 代理IPV4/IPV6优先 | 订阅节点统一 IP 版本偏好 | 关 |
| 链式代理 | 自定义节点经「链式中转」落地 | 关 |

## 图标

40 枚「簪花印」SVG（策略组 + 地区 + 工具类 + 2 枚备用），桃粉底白符，统一规范化至 1024×1024 画布，jsdelivr 全局 CDN 直链：

```text
https://fastly.jsdelivr.net/gh/JokerXiaoMo/FlClash-Tuned@main/Icons/svg/<Name>.svg
```

- 覆写脚本自动为所有策略组配置图标，FlClash 中直接可见
- 如需自定义：FlClash → 配置 → 编辑 → **覆写 → 自定义 → 图标**，粘贴上面的链接即可
- 图标体系与 [taobai-zanhua](https://github.com/JokerXiaoMo/taobai-zanhua) 同源；来源与许可证见 [Icons/README.md](Icons/README.md)

## 目录结构

```text
FlClash-Tuned/
├── Script/                  # mihomo 覆写脚本（全量/精简）
├── Config/                  # 静态 mihomo 配置（全量/精简）
├── Icons/svg/               # 40 枚 1024×1024 簪花印图标
├── Rules/                   # 下载类应用直连规则清单
├── Test/                    # 自动化测试（182 项）
├── .github/workflows/       # CI：自动化测试
└── AGENT.md                 # 维护者规约
```

## 测试

```bash
node Test/run-tests.js        # 全部测试（推荐 Node ≥ 16）
npm --prefix Test install     # 可选：启用 ES2020 / QuickJS 兼容性检查后重跑
```

## 常见问题

**Q：节点显示「内鬼」/解析到垃圾线路？**
机场用了私有 DNS 或 hosts 映射节点域名。本脚本已内置自动处理，遇到无法解析的节点可提 Issue 附上（脱敏后的）节点域名。

**Q：为什么必须关闭 FlClash 的 DNS 覆写？**
脚本生成整套无泄露 DNS 配置；FlClash 的 DNS 覆写开启时会用 App 补丁覆盖它，两者叠加会产生意想不到的行为。

**Q：TUN 模式用不用开？**
随意。TUN 完全由 FlClash 控制，本套件不干预。Windows 下解决 DNS 泄露建议开启 TUN 的严格路由。

**Q：图标在 FlClash 里不显示？**
首次加载需联网拉取 jsdelivr；确认系统代理正常后重启 FlClash 重试。

## 致谢与许可

- [AIsouler/MyClash](https://github.com/AIsouler/MyClash)（MIT）——特调思路与覆写脚本蓝本
- [JokerXiaoMo/taobai-zanhua](https://github.com/JokerXiaoMo/taobai-zanhua)（MIT）——「簪花印」图标体系（姐妹项目）
- [chen08209/FlClash](https://github.com/chen08209/FlClash)（GPL-3.0）——适配目标（本项目不含 FlClash 代码，仅为其提供配置/脚本/图标）
- [MetaCubeX/meta-rules-dat](https://github.com/MetaCubeX/meta-rules-dat)——规则集

本项目以 [MIT](LICENSE) 协议开源。使用即代表你同意遵守所在地法律法规，本项目仅用于学习与技术研究。

---

<div align="center">灵感源自 MyClash · 图标源自桃白簪花 · 为 FlClash 而调 · FlClash-Tuned</div>
