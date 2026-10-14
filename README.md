# DeepSeek Harness for Linux（社区打包）

[English](#english) | 简体中文

> ⚠️ 本项目为**非官方**社区打包，与 DeepSeek 无隶属关系。产物为 unsigned 构建。

将官方 [DeepSeek Harness](https://github.com/deepseek-ai/deepseek-harness) 桌面端带到 Linux。  
上游目前不支持 Linux 桌面发行（官方 README：*"Linux is not a supported Desktop release target"*），  
本项目基于社区 [ffyfox/dsh-desktop-linux](https://github.com/ffyfox/dsh-desktop-linux) 的补丁系列，  
从上游 `dsh-v0.2.1-alpha.2` 源码构建出可安装的 deb 包。

---

## ✨ 特性

- 🖥️ 与官方 Windows/macOS 桌面端一致的 Electron 应用：渲染走自有 `dsh-app://` 协议，不依赖本地 Web 服务
- 📦 内置 Node 24 / pnpm 11 / Python 3.12 运行时，**不依赖系统 Node**
- 🔒 独占 `~/.dsh/profiles/desktop`，与 CLI 的 web profile 互不干扰；会话与凭据仍共享 `~/.dsh`
- 🧩 完整技能（skills）体系：Office 文档、数据分析等开箱即用
- 🫥 关窗隐藏到托盘，后台任务不中断；托盘菜单可完全退出（补丁 0013）
- 🛡️ 内核支持非特权 user namespace 时使用 namespace 沙箱 + seccomp，否则回退 setuid `chrome-sandbox`（postinst 自动判断）

## 📥 安装

Debian / Ubuntu（x86_64）：

```bash
sudo apt install ./deepseek-harness-0.2.1-alpha.2-linux-amd64-unsigned.deb
```

安装后应用菜单出现 **DeepSeek Harness**，`dsh://` 链接自动由它接管。

## 📋 已知限制

- **Unsigned 构建**：未签名，部分发行版安装时会有提示
- **无自动更新**：上游更新通道只认 `desktop-win` / `desktop-mac`，Linux 版不轮询更新，升级需重新安装新 deb
- **GNOME 托盘**：需安装 `gnome-shell-extension-appindicator`（Ubuntu 自带；Debian/Fedora 需手动安装并注销重登）
- **仅 x86_64**；未验证 aarch64
- 平台侧客户端身份会被识别为 `desktop-mac`（上游类型联合的既有行为）

## ❓ FAQ

**Q: 窗口打开太小 / 高分屏下内容太窄？**  
窗口可以正常拖边框调整大小（最小宽度 520px），也可最大化；用 `Ctrl` + `=` / `Ctrl` + `-` 缩放内容。

**Q: 关闭窗口后程序还在运行？**  
这是上游设计：关窗隐藏到托盘，后台任务继续。完全退出走托盘菜单、应用菜单 `Application → Quit` 或 `Ctrl+Q`。

**Q: 如何在终端使用 dsh CLI？**  
应用菜单没有“安装命令行工具”入口（上游只实现了 macOS/Windows），可手动使用  
`resources/app/dsh/node_modules/@deepseek-ai/dsh/lib/bin.js`，配合 `resources/runtime/primary-runtime` 内置 node。

## 🙏 致谢

- [ffyfox/dsh-desktop-linux](https://github.com/ffyfox/dsh-desktop-linux) —— Linux 打包补丁系列与构建脚本
- [DeepSeek Harness](https://github.com/deepseek-ai/deepseek-harness) —— 上游应用本体

## 📄 许可

补丁与打包脚本遵循上游社区项目许可（MIT）；DeepSeek Harness 本体版权归 DeepSeek 所有。  
本项目不分发修改后的上游代码，仅提供构建脚本与补丁；二进制产物由使用者自行从源码构建。

---

<a id="english"></a>

## English

Unofficial community packaging that brings the official [DeepSeek Harness](https://github.com/deepseek-ai/deepseek-harness) desktop app to Linux, built from upstream `dsh-v0.2.1-alpha.2` sources via the patch series of [ffyfox/dsh-desktop-linux](https://github.com/ffyfox/dsh-desktop-linux).

```bash
sudo apt install ./deepseek-harness-0.2.1-alpha.2-linux-amd64-unsigned.deb
```

Features: self-contained runtimes (Node 24 / pnpm 11 / Python 3.12), dedicated desktop profile, tray with close-to-tray behavior, namespace sandbox. Known limitations: unsigned build, no auto-update, tray requires an appindicator extension on GNOME, x86_64 only.
