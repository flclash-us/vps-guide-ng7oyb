# Clash TUN 模式配置完全指南

TUN 模式是 Clash 的高级功能，可接管系统所有流量，实现真正的全局代理。

## 什么是 TUN 模式

普通代理模式只影响支持 SOCKS/HTTP 代理的应用程序。TUN 模式通过创建虚拟网卡，将所有流量导入 Clash，实现：

- 全局代理（所有应用）
- 游戏加速（UDP 优化）
- 移动应用代理
- 防止 DNS 泄漏

## Windows (Clash Verge / Clash for Windows)

Clash for Windows 原生支持 TUN 模式：

1. 设置 > 开启 TUN Mode
2. 安装虚拟网卡驱动（首次需授权）
3. 配置生效

推荐使用 [Clash Verge](https://github.com/clash-verge/clash-verge)，TUN 体验更流畅。

## Linux / OpenWrt

Linux 下使用 `clash-linux` 配合 TUN：

```yaml
tun:
  enable: true
  stack: system
  auto-route: true
  auto-detect-interface: true
```

## Android (ClashMeta)

ClashMeta 支持 Android TUN：

1. 设置 > TUN 模式 > 开启
2. 授予 VPN 权限
3. 游戏加速场景推荐开启

## 游戏加速优化

TUN 模式配合以下配置可优化游戏体验：

```yaml
rules:
  - MATCH, Gaming
proxy-groups:
  - name: Gaming
    type: url-test
    proxies: [...]
    url: "http://www.gstatic.com/generate_204"
    interval: 300
```

## 常见问题

**TUN 模式耗电？** Android 上 TUN 会略微增加耗电，建议按需开启。

**和 VPN 冲突？** 同时只能运行一个 VPN/TUN，关闭其他 VPN 后再使用。

---

推荐工具：

- [Clash for Windows](https://clashforwindows.site/) - 带 TUN 模式的 Clash 客户端
- [ClashMI](https://clashmi.site/) - 轻量级选择
- [FlClash](https://flclash.us/) - 现代 TUN 实现
