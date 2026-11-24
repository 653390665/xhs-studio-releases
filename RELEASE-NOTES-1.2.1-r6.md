# 版本 1.2.1-r6

## 下载

| 平台 | 文件 | SHA-256 |
|---|---|---|
| Windows 10 / 11 (x64) | `XHS-Studio-1.2.1-r6-Setup.exe` | `74581370D38449988C555D058FBA3F502087D21617673C36343ABECD118DB335` |
| macOS 预览版 | `XHS-Studio-1.2.1-r6-macOS-Preview.dmg` | `6BB0B7F99144F26F0216DC2895CC1BB9DE1462F24177CA34848876D26390153F` |

## 这一版

r6 在 1.2.1（CSS 类名撞车修复版）基础上修了两处界面问题：

- **安装窗口按钮可见**：旧安装器把窗口高度写死成 `560x300`，系统缩放 133% 时
  「取消 / 开始安装」整行被裁在窗口外。现在按内容实测尺寸，并声明 DPI 感知。
- **宽屏不再空一块**：内容区最大宽度 1320px，在 2K / 4K 屏上不再出现整片右侧留白。

其它与 1.2.1 一致：

- 修复 `写法与能力` 页整页发灰闪烁（`.sk` 与骨架屏类名撞车）
- 修复 `设置 → 运行状态 → 任务记录` 整块不显示（`.tp` 与顶部进度条撞车）
- 修复弹窗与 Markdown 共用 `.md` / `.md__body` 导致的正文多出 20px 内边距
- 10 条方法论 Skill 随包发布，装好即启用
- 11 个写作模板 + 8 个文字卡版式

## ⚠️ 未签名

没有商业代码签名证书，Windows SmartScreen 与 macOS Gatekeeper 都会拦一次。

**Windows**：双击 → 「更多信息」→「仍要运行」。被直接拦下时先
`Unblock-File .\XHS-Studio-1.2.1-r6-Setup.exe`。

**macOS**：系统设置 → 隐私与安全性 → 「已阻止 XHS Studio 以保护 Mac」→ **仍要打开**；
或终端执行 `xattr -dr com.apple.quarantine "/Applications/XHS Studio.app"`。

真实性请用上面的 SHA-256 核对，不要依据系统弹窗判断。

## 安装

Windows：装到 `%LOCALAPPDATA%\Programs\XHSStudio`，不需要管理员权限。
覆盖安装不会动 `%LOCALAPPDATA%\XHSStudio\` 里的用户数据。

macOS：拖 `XHS Studio.app` 到「应用程序」。

## 从 1.2.1 升级

直接装新的就行。数据层零改动，不需要迁移。

## 已知限制

- macOS 版为预览，发布链路以 Windows 为准
- 无自动更新
- 无代码签名
