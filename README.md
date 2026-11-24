# XHS Studio · 安装包下载

小红书内容运营工作台（Windows / macOS 预览版）。
采集 → 提炼 → 写稿 → 发布，全流程在一个本地应用里完成。

**这是发行仓库**：只放安装包与校验值，源码不在这个仓库里。

---

## 下载

| 平台 | 文件 | 大小 |
|---|---|---|
| Windows 10 / 11 (x64) | [`XHS-Studio-1.2.1-r6-Setup.exe`](../../releases/latest) | 228 MB |
| macOS（Apple Silicon / Intel 预览版） | [`XHS-Studio-1.2.1-r6-macOS-Preview.dmg`](../../releases/latest) | 388 MB |

进 [Releases](../../releases) 页面下载，同一页面附 `.sha256` 校验文件。

### 校验值（SHA-256）

```
74581370D38449988C555D058FBA3F502087D21617673C36343ABECD118DB335  XHS-Studio-1.2.1-r6-Setup.exe
6BB0B7F99144F26F0216DC2895CC1BB9DE1462F24177CA34848876D26390153F  XHS-Studio-1.2.1-r6-macOS-Preview.dmg
```

下载后请核对一次。**校验通过 = 文件在传输中没被改动**，这是本项目目前能做的最强保证。

---

## ⚠️ 未签名：系统会拦一次，这是预期的

这两个包**没有购买商业代码签名证书**，所以：

- Windows 会弹 SmartScreen「Windows 已保护你的电脑」
- macOS 会提示「无法验证开发者 / 已阻止以保护 Mac」

这**不等于文件有毒**，只表示发布者没有向 Microsoft / Apple 付费注册身份。
真实性请用上面的 SHA-256 判断，而不是看系统弹窗。

### Windows：怎么继续装

1. 双击 `XHS-Studio-1.2.1-r6-Setup.exe`
2. 弹出「Windows 已保护你的电脑」→ 点左侧 **更多信息**
3. 点 **仍要运行**

被 SmartScreen 直接拦下、没有「更多信息」时：

```powershell
# 右键 exe → 属性 → 勾选「解除锁定」→ 确定
# 或命令行：
Unblock-File .\XHS-Studio-1.2.1-r6-Setup.exe
```

装的是当前用户目录（`%LOCALAPPDATA%\Programs\XHSStudio`），**不需要管理员权限**。

### macOS：怎么继续打开

**方式一（推荐）**：系统设置 → 隐私与安全性 → 滚到底部 → 看到「已阻止 XHS Studio 以保护 Mac」→ 点 **仍要打开** → 再确认一次「打开」。

**方式二**：终端里去掉隔离标记

```bash
xattr -dr com.apple.quarantine /Applications/XHS\ Studio.app
```

> macOS 版目前是**预览版**：能装能开，但发布链路仍以 Windows 为准。

---

## 安装后：四步开始用

装完启动，浏览器打开 `http://127.0.0.1:8000`，首次注册一个本机账号。

1. **配模型**（必做）：设置 → 模型 → 填 DeepSeek 等兼容 OpenAI 的 API Key
2. **绑账号**（必做）：设置 → 账号 → 扫码登录小红书
   （要用「自动运营」就在扫码时勾上「同时获取创作中心账号」）
3. **采素材**：素材 → 采集 → 搜关键词 → 勾几篇存进样本库
4. **写稿**：写稿 → 填主题 → 生成

素材页和样本库不需要模型，可以先点开看。

---

## 这个版本里有什么

- **5 个一级入口**：今日 / 素材 / 写稿 / 发布 / 设置
- **写稿三栏**：素材 → 正文 → 配图与检查，首屏不需要先选东西
- **10 条方法论 Skill** 随包发布（账号定位、对标拆解、选题标题、写稿改稿、排期复盘、视觉生产），装好即启用，按任务自动注入
- **11 个写作模板 + 8 个文字卡版式**，离线可用
- **内置 Node.js 运行时**：小红书请求签名用，不用另装
- 首次启动自动建库、自动生成加密密钥，全部在本机用户目录

不含任何账号、Cookie、API Key 或历史数据。

### 系统要求

- Windows 10 / 11（64 位）或 macOS 12+
- 4 GB 内存以上
- 约 1.2 GB 磁盘（安装包 + 解压后）
- **不需要**预装 Python、Node.js、数据库

---

## 已知限制

- 没有代码签名，首次运行必然被拦一次（见上）
- 没有自动更新，新版本要手动下载覆盖安装（覆盖不会动你的数据）
- 只有 Windows 版经过完整验证；macOS 版为预览
- 发布动作默认需要你手动确认，不默认无人值守

---

## 卸载

- Windows：设置 → 应用 → XHS Studio → 卸载，或运行安装目录里的 `Uninstall.ps1`
- macOS：把 `XHS Studio.app` 拖进废纸篓

用户数据在下面这些位置，卸载不会自动删除：

```
Windows:  %LOCALAPPDATA%\XHSStudio\
macOS:    ~/Library/Application Support/XHSStudio/
```

---

## 安全说明

- 所有数据存在本机，默认不向第三方上传
- API Key 用本机生成的 Fernet 密钥加密后入库
- 应用只监听 `127.0.0.1`，不对局域网开放
- 采集与发布走的是你自己的小红书账号会话
