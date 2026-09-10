# WLOC Self-hosted

Apple 网络定位（WLOC）Surge 自托管副本。

本仓库用于把 WLOC 核心文件托管在自己的 GitHub 下，避免上游仓库删除、重命名或 Raw 地址失效后影响 Surge。

## Surge 订阅

仓库改为 Public 并完成首次同步后，在 Surge 中使用：

```text
https://raw.githubusercontent.com/roninriddle/wloc/main/wloc.sgmodule
```

核心脚本：

```text
https://raw.githubusercontent.com/roninriddle/wloc/main/wloc.js
https://raw.githubusercontent.com/roninriddle/wloc/main/wloc-settings.js
```

## 更新

进入 GitHub Actions，运行 **Sync WLOC Upstream** 即可从当前维护版本同步，并自动把模块内的上游地址改成本仓库地址。

> 注意：当前仓库如果是 Private，Surge 无法匿名读取 Raw 文件。用于 Surge 订阅时请设为 Public。

## 来源

当前同步源：`zxishere/wloc`。该版本在 2026-09-10 仍有维护提交，并已包含自托管脚本、扩展 WLOC 域名和 iOS 新版本说明。

仅供自有设备测试和学习使用。开启 HTTPS MITM/解密前请自行评估安全风险。
