# WLOC Self-hosted

Apple 网络定位（WLOC）Surge 自托管版本。

这个仓库把 WLOC 核心脚本和自定义控制台放在自己的 GitHub 下，避免上游 Raw 地址变化影响使用，同时保留独立的 UI、Surge 模块和 PWA 配置。

## Surge 模块

```text
https://raw.githubusercontent.com/roninriddle/wloc/main/wloc.sgmodule
```

核心脚本：

```text
https://raw.githubusercontent.com/roninriddle/wloc/main/wloc.js
https://raw.githubusercontent.com/roninriddle/wloc/main/wloc-settings.js
```

## WLOC 控制台

```text
https://roninriddle.github.io/wloc/
```

控制台当前提供：

- 地图选点、地名搜索、坐标输入
- 收藏位置
- 收藏位置一键“使用”并直接写入设备
- 模块连接 / 已保存目标 / 系统定位三层状态诊断
- 读取 iPhone 当前系统定位并计算与 WLOC 目标的距离
- iOS 26+ 重启切换向导
- 恢复真实定位
- PWA / 添加到主屏幕
- 显示当前同步的上游核心脚本版本

## PWA

在 iPhone Safari 中打开控制台后：

**分享 → 添加到主屏幕**

之后可像独立 App 一样打开 WLOC 控制台。`manifest.json`、`sw.js` 和 `icon.svg` 由本仓库独立维护，不会被上游同步覆盖。

## 上游同步策略

GitHub Actions：`Sync WLOC Core`

- 每天自动检查一次，也可以手动运行。
- 当前核心脚本来源：`zxishere/wloc`。
- 只同步 `wloc.js` 和 `wloc-settings.js`。
- 同步前会检查核心文件是否存在并包含预期标记。
- `index.html`、`wloc.sgmodule`、PWA 文件和本仓库自定义逻辑不会被上游覆盖。
- 每次同步会更新 `upstream-version.json`，控制台底部会显示当前核心提交。

这种方式把“核心脚本更新”和“自定义控制台”分离，避免一次上游同步把本地优化全部覆盖。

## iOS 26+

iOS 26+ 的定位缓存更强。写入新坐标后，如果系统定位没有切换，建议按控制台中的向导执行：

1. 写入目标坐标。
2. 关闭定位服务。
3. 重启 iPhone。
4. 开机后先启动 Surge。
5. 再开启定位服务。
6. 在控制台中点击“验证系统定位”。

如果 GPS 信号很强，系统仍可能优先采用 GPS；室内或 GPS 较弱环境更适合验证 WLOC 网络定位结果。

## 文件结构

```text
index.html               自定义 WLOC 控制台
wloc.sgmodule            Surge 模块
wloc.js                  WLOC 核心响应脚本（自动同步）
wloc-settings.js         设置/查询脚本（自动同步）
manifest.json            PWA Manifest
sw.js                    PWA Service Worker
icon.svg                 PWA 图标
upstream-version.json    当前核心脚本来源与提交
.github/workflows/
  sync-wloc.yml          核心脚本自动同步
```

仅供自有设备测试和学习使用。开启 HTTPS MitM/解密前请自行评估安全风险。
