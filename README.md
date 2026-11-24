# XHS Studio · 发行说明

小红书内容运营工作台。**安装包全部由 GitHub Actions 从源码构建**，
构建过程在 Actions 里逐步可查。

---

## 下载最新版

### 👉 [**v1.2.2（最新）**](https://github.com/653390665/xhs-studio/releases/latest)

| 平台 | 文件 | 大小 |
|---|---|---|
| Windows 10 / 11 (x64) | `XHS-Studio-1.2.2-Setup.exe` | 214.5 MB |

```
SHA-256  AD99CBFE62E2D4D3DDF4C044437DB3CD9CE2B67EFEDBC4771B44EF2DAAF0F059
```

下载后请核对一次。校验通过 = 文件在传输中没被改动。

### 校验方法

```powershell
# Windows PowerShell
Get-FileHash .\XHS-Studio-1.2.2-Setup.exe -Algorithm SHA256
```

```bash
# macOS / Linux
shasum -a 256 XHS-Studio-1.2.2-Setup.exe
```

和上面那串对比，一致即可。

---

## ⚠️ 未签名：系统会拦一次，这是预期的

安装包**没有买商业代码签名证书**，所以 Windows 会弹 SmartScreen
「Windows 已保护你的电脑」。

这**不等于文件有毒**，只表示发布者没有向 Microsoft 付费注册身份。
真实性请用上面的 SHA-256 判断，而不是看系统弹窗。

### 怎么继续装

1. 双击 `XHS-Studio-1.2.2-Setup.exe`
2. 弹出「Windows 已保护你的电脑」→ 点左侧 **更多信息**
3. 点 **仍要运行**

被 SmartScreen 直接拦下、没有「更多信息」按钮时：

```powershell
# 右键 exe → 属性 → 勾选「解除锁定」→ 确定
# 或命令行：
Unblock-File .\XHS-Studio-1.2.2-Setup.exe
```

装的是当前用户目录（`%LOCALAPPDATA%\Programs\XHSStudio`），**不需要管理员权限**。

---

## 安装后：四步开始用

装完启动，浏览器自动打开 `http://127.0.0.1:8000`，首次注册一个本机账号。

1. **配模型**（必做）：设置 → 模型 → 填 DeepSeek 等兼容 OpenAI 的 API Key
2. **绑账号**（必做）：设置 → 账号 → 扫码登录小红书
   （要用「自动运营」就在扫码时勾上「同时获取创作中心账号」）
3. **采素材**：素材 → 采集 → 搜关键词 → 勾几篇存进样本库
4. **写稿**：写稿 → 填主题 → 生成

素材页和样本库不需要模型，可以先点开看。

### 抖音视频转文字：需要先装 ffmpeg

安装包**不带 ffmpeg**。要用抖音采集转口播文稿：

```powershell
winget install Gyan.FFmpeg
```

或从 ffmpeg.org 下载后把 `bin` 加进 PATH。确认能跑 `ffmpeg -version` 即可。

没装时「素材 → 采集」顶部会显示「转写环境未就绪 · 缺 ffmpeg」，
不会假装能用。转写模型（faster-whisper small）在第一次转写时自动下载，约 500 MB。

---

## 这个版本里有什么

- **5 个一级入口**：今日 / 素材 / 写稿 / 发布 / 设置
- **写稿三栏**：素材 → 正文 → 配图与检查，首屏不需要先选东西
- **10 条方法论 Skill** 随包发布（账号定位、对标拆解、选题标题、写稿改稿、
  排期复盘、视觉生产），装好即启用，按任务自动注入
- **11 个写作模板 + 8 个文字卡版式**，离线可用
- **内置 Node.js 20 LTS 运行时**：小红书请求签名用，不用另装
- 首次启动自动建库、自动生成加密密钥，46 个迁移自动跑完

不含任何账号、Cookie、API Key 或历史数据。

### 系统要求

- Windows 10 / 11（64 位）
- 4 GB 内存以上
- 约 1.2 GB 磁盘（安装包 + 解压后）
- **不需要**预装 Python、Node.js、数据库

---

## 已知限制

- **无代码签名**，首次运行必然被拦一次（见上）
- **无自动更新**，新版本要手动下载覆盖安装（覆盖不会动你的数据）
- **只有 Windows 版**。这个仓库不含 macOS 构建链路
- 发布动作默认需要手动确认，不默认无人值守

---

## 卸载

设置 → 应用 → XHS Studio → 卸载，或运行安装目录里的 `Uninstall.ps1`。

用户数据在下面这个位置，卸载**不会**自动删除：

```
%LOCALAPPDATA%\XHSStudio\
```

彻底清除时手动删掉该目录。注意里面有 `secret.key`，
删了之后要把模型 Key 和账号 Cookie 重新填一遍。

---

## 关于这个仓库

这里是**发行仓库**：只放安装包与校验值。

源码在 [653390665/xhs-studio](https://github.com/653390665/xhs-studio)，
构建流水线在 [.github/workflows/build.yml](https://github.com/653390665/xhs-studio/blob/main/.github/workflows/build.yml)。

每一版都能这样查证：

```
Actions → Build Installer → 选某次 run
  → 看 commit、看测试结果、看 verify 步骤的实际输出
```

历史版本里的安装包只要在这里能下到，就说明它出自哪次 CI 构建。

---

## 安全说明

- 所有数据存在本机，默认不向第三方上传
- API Key 用本机生成的 Fernet 密钥加密后入库
- 应用只监听 `127.0.0.1`，不对局域网开放
- 采集与发布走的是你自己的小红书账号会话
