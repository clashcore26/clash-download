# Clash for Windows Guide

## Clash for Windows 完整使用指南

Clash for Windows 是 Clash 客户端生态中较为经典的 Windows 图形界面客户端。本指南从下载安装到日常使用，整理 Clash for Windows 的配置导入、代理切换、系统代理、规则分流、DNS、TUN 以及常见问题。

如果你刚开始接触 Clash for Windows，可以按照本文的顺序逐步配置；如果已经安装完成，也可以直接跳转到对应章节查找问题。

---

## 📌 目录

* [Clash for Windows 是什么](#clash-for-windows-是什么)
* [版本说明](#版本说明)
* [下载安装](#下载安装)
* [首次启动](#首次启动)
* [导入配置文件](#导入配置文件)
* [Profiles 配置管理](#profiles-配置管理)
* [Proxies 代理设置](#proxies-代理设置)
* [Proxy Groups 策略组](#proxy-groups-策略组)
* [开启 System Proxy](#开启-system-proxy)
* [Rules 规则分流](#rules-规则分流)
* [DNS 设置](#dns-设置)
* [TUN Mode](#tun-mode)
* [常见使用场景](#常见使用场景)
* [连接失败排查](#连接失败排查)
* [速度慢排查](#速度慢排查)
* [无法打开网页](#无法打开网页)
* [卸载 Clash for Windows](#卸载-clash-for-windows)
* [版本维护说明](#版本维护说明)
* [相关文档](#相关文档)

---

## Clash for Windows 是什么

Clash for Windows 通常简称 **CFW**，是一款基于 Clash 内核的 Windows 图形界面客户端。

它将 Clash 的配置、代理节点、策略组和规则等功能整合到一个桌面应用中。

对于普通用户来说，可以通过图形界面完成：

* 导入配置
* 选择代理
* 切换策略组
* 设置系统代理
* 查看连接
* 配置规则
* 调整 DNS
* 使用 TUN

因此，使用 Clash for Windows 时，并不需要一开始就理解所有 YAML 参数。

先掌握客户端的基本界面，再逐步理解配置文件和规则，会更容易上手。

---

## 版本说明

本仓库收录了 Clash for Windows 相关资料，同时整理经典版本信息。

目前重点记录：

**Clash for Windows v0.20.39**

v0.20.39 是 Clash for Windows 原项目的最终官方版本。

如果你需要查找版本资料，可以先查看：

* [Clash Download](../clash-download.md)
* [v0.20.39 Release](https://github.com/clashcore26/clash-download/releases/tag/v0.20.39)

> Clash for Windows 原项目已经停止维护，因此安装旧版本时需要特别注意 Windows 兼容性、安全性以及软件来源。

---

## 下载安装

下载 Clash for Windows 时，首先确认自己的 Windows 系统和 CPU 架构。

一般 Windows 10 / Windows 11 64 位电脑选择 x64 版本即可。

下载完成后：

1. 获取对应版本安装文件。
2. 双击安装程序。
3. 根据安装程序提示完成安装。
4. 启动 Clash for Windows。
5. 等待客户端初始化完成。

如果 Windows 弹出安全提示，应先确认安装文件来源，再决定是否继续。

### 下载入口

可以从本仓库的 Releases 页面查看版本资料：

**[Clash for Windows Releases](https://github.com/clashcore26/clash-download/releases)**

---

## 首次启动

第一次打开 Clash for Windows 后，可以先认识几个主要页面。

常见功能区域包括：

| 页面          | 主要功能   |
| ----------- | ------ |
| General     | 基础设置   |
| Proxies     | 代理与策略组 |
| Profiles    | 配置文件   |
| Logs        | 日志     |
| Connections | 当前连接   |
| Rules       | 当前规则   |

不同版本的界面可能存在细微差异。

第一次使用时，不建议立即修改大量高级参数。

可以按照：

```text
导入配置
↓
选择配置
↓
选择代理
↓
开启 System Proxy
↓
测试网络
```

这个顺序完成基础配置。

---

## 导入配置文件

Clash for Windows 的正常工作依赖配置文件。

配置文件通常包含：

```text
代理节点
策略组
规则
DNS
其他网络参数
```

打开 **Profiles** 页面后，可以添加或导入 Clash 配置。

配置文件可能来自：

* 本地 YAML 文件
* URL 配置
* 已有的 Clash 配置

导入以后，需要确认配置已经成功加载。

如果配置文件无法使用，可以检查：

* YAML 格式是否正确
* URL 是否有效
* 配置是否包含必要字段
* 配置文件是否适用于当前 Clash 内核

---

## Profiles 配置管理

Profiles 可以理解为 Clash for Windows 的配置文件管理区域。

如果你有多个配置，可以分别保存。

例如：

```text
daily.yaml
work.yaml
testing.yaml
```

不同配置可以拥有不同的：

* 节点
* 策略组
* 规则
* DNS
* 网络参数

### 建议

不要为了测试一个参数就直接修改唯一的配置文件。

更好的方式是保留一个可以正常工作的基础配置，然后复制一份进行测试。

这样出现问题时，可以快速恢复。

---

## Proxies 代理设置

进入 **Proxies** 页面后，可以看到配置文件中的代理和策略组。

例如：

```text
Proxy
├── Node A
├── Node B
└── Node C

Auto
├── Node A
├── Node B
└── Node C
```

如果配置文件包含策略组，实际使用时通常选择策略组，而不是每次手动选择单个节点。

### 基础测试方法

选择一个可用代理后，打开浏览器测试：

1. 普通网页
2. HTTPS 网站
3. 国内网站
4. 需要代理的网站

如果只有部分网站可以访问，需要继续检查 Rules 和 DNS。

---

## Proxy Groups 策略组

策略组决定流量最终使用哪个代理。

常见类型包括：

* 手动选择
* 自动选择
* URL-Test
* Fallback
* Load-Balance

简单配置可以使用：

```text
Proxy
├── Node A
├── Node B
└── Node C
```

更复杂的配置可能是：

```text
Proxy
├── Auto
├── Singapore
├── Japan
├── US
└── DIRECT
```

实际选择哪种策略取决于配置文件设计。

---

## 开启 System Proxy

如果希望 Windows 中支持系统代理的应用通过 Clash 工作，可以打开：

**General → System Proxy**

开启以后，Windows 系统代理会指向 Clash 的本地代理端口。

基础工作流程：

```text
Windows 应用
     ↓
System Proxy
     ↓
Clash for Windows
     ↓
Rules
     ↓
Proxy Group
     ↓
目标网络
```

### 如果开启后没有网络

不要马上修改所有设置。

首先：

1. 关闭 System Proxy。
2. 确认浏览器本身可以正常联网。
3. 确认 Clash 配置已经加载。
4. 检查 Proxies 是否有可用节点。
5. 再重新开启 System Proxy。

---

## Rules 规则分流

Rules 决定不同网络请求应该走哪里。

一个简单的规则可能类似：

```yaml
rules:
  - DOMAIN-SUFFIX,example.com,Proxy
  - GEOIP,CN,DIRECT
  - MATCH,Proxy
```

规则通常按照从上到下的顺序进行匹配。

因此规则顺序非常重要。

### 常见规则类型

```text
DOMAIN
DOMAIN-SUFFIX
DOMAIN-KEYWORD
IP-CIDR
GEOIP
RULE-SET
MATCH
```

例如：

```text
国内网站 → DIRECT
国外网站 → Proxy
指定域名 → 指定策略组
未匹配流量 → MATCH
```

如果发现某个网站没有按照预期走代理，首先查看 Rules，而不是立即更换节点。

---

## DNS 设置

DNS 负责域名解析。

Clash for Windows 中 DNS 设置出现问题时，可能表现为：

* 网站打不开
* 域名解析失败
* 页面加载很慢
* 某些域名正常，某些域名异常

排查 DNS 时，可以依次检查：

```text
DNS 配置
↓
nameserver
↓
fallback
↓
fake-ip
↓
fake-ip-filter
↓
系统 DNS
```

如果使用 Fake-IP，还需要确认相关域名是否应该加入过滤列表。

---

## TUN Mode

TUN 是 Clash 使用过程中比较高级的功能。

开启 TUN 后，客户端可以处理比普通系统代理更多的网络流量。

但 TUN 同时涉及：

* 虚拟网络接口
* 路由
* DNS
* 系统权限
* 网络适配器

因此，出现问题时需要比 System Proxy 更仔细地排查。

### 开启 TUN 前

建议先确认：

* 普通 System Proxy 可以正常工作
* 配置文件正常
* 代理节点正常
* DNS 没有明显错误

然后再测试 TUN。

### TUN 开启后断网

可以按照：

```text
关闭 TUN
↓
确认 System Proxy 正常
↓
检查 DNS
↓
检查 TUN 配置
↓
检查 Windows 网络适配器
↓
重新开启 TUN
```

不要同时修改 DNS、Rules、TUN 和代理节点，否则很难判断真正的问题来源。

---

## 常见使用场景

### 日常浏览

推荐保持简单：

```text
Clash
↓
Profiles
↓
选择配置
↓
Proxies
↓
选择策略组
↓
System Proxy
```

不需要为了普通网页访问打开大量高级功能。

---

### 开发环境

开发工具可能不会完全遵循 Windows 系统代理。

例如：

* Git
* npm
* Python
* Docker
* Terminal
* IDE

这类软件遇到网络问题时，需要分别确认它们是否支持系统代理，或者是否需要单独配置代理。

因此：

> Clash 正常，并不代表所有开发工具都会自动使用 Clash。

---

### 游戏

游戏是否使用 Clash，需要根据游戏自身网络机制判断。

部分游戏遵循系统代理，部分游戏使用自己的网络连接方式。

如果开启 Clash 后游戏网络没有变化，不一定是 Clash 配置错误。

---

## 连接失败排查

遇到 Clash for Windows 无法连接时，可以按照以下顺序检查。

### 第一步：确认客户端运行

确认 Clash for Windows 正常启动。

### 第二步：确认配置

进入 Profiles，检查配置是否已经加载。

### 第三步：确认代理

进入 Proxies，检查是否存在可用代理。

### 第四步：检查策略组

确认当前策略组不是：

```text
DIRECT
```

或者一个已经失效的节点。

### 第五步：检查 Rules

确认目标网站没有被错误规则匹配。

### 第六步：检查 DNS

如果日志显示域名解析错误，再进一步检查 DNS。

---

## 速度慢排查

Clash 速度慢可以从多个方向判断。

首先区分：

```text
节点速度
网络线路
DNS
代理协议
客户端
规则
目标网站
```

可以进行简单测试：

1. 更换一个节点。
2. 测试同一网站。
3. 比较不同节点延迟。
4. 检查 DNS。
5. 查看 Connections。
6. 查看 Logs。

如果只有一个节点速度慢，通常没有必要修改整个 Clash 配置。

---

## 无法打开网页

如果浏览器完全无法访问网页：

### 检查 System Proxy

确认系统代理是否指向 Clash。

### 检查代理端口

确认 Clash 正常监听本地代理端口。

### 检查配置

确认 Profiles 中的配置没有报错。

### 检查策略组

确认当前策略组存在可用节点。

### 检查 DNS

如果可以连接 IP，但是域名打不开，可以重点检查 DNS。

---

## Logs 与 Connections

排查问题时，**Logs** 和 **Connections** 非常有价值。

### Logs

可以观察：

* DNS 请求
* 配置加载
* 网络连接
* 错误信息

### Connections

可以观察当前应用产生的连接。

当某个网站访问异常时，可以先打开 Connections，然后访问目标网站。

如果能够看到对应连接，就可以进一步判断：

* 使用了哪个规则
* 连接到哪个目标
* 使用哪个策略组

这通常比反复修改配置更有效。

---

## 卸载 Clash for Windows

如果确定不再使用 Clash for Windows，可以先关闭客户端，然后通过 Windows 的应用管理功能卸载。

如果卸载后仍然出现网络代理问题，需要额外检查：

* Windows System Proxy
* TUN / 虚拟网络适配器
* DNS
* 系统网络设置

建议卸载前先关闭 Clash 的系统代理功能。

---

## 版本维护说明

Clash for Windows 已经属于经典客户端。

本仓库保留相关资料的主要目的包括：

* 方便查找历史版本
* 方便旧设备用户查阅
* 保存使用经验
* 记录 Clash 客户端生态的发展过程

如果你正在选择新的 Clash / Mihomo 客户端，不建议只根据软件名称选择，还应该查看：

* 项目是否仍在维护
* 使用的内核
* 系统兼容性
* 最新版本
* 配置兼容性
* Issue 活跃程度

---

## 相关文档

* [Clash Download](../clash-download.md)
* [Clash Installation Guide](installation.md)
* [Clash Configuration](configuration.md)
* [Clash DNS Guide](dns.md)
* [Clash TUN Guide](tun-mode.md)
* [Clash Connection Troubleshooting](connection-failed.md)
* [Clash Speed Troubleshooting](slow-speed.md)

### GitHub Releases

* [Latest Releases](https://github.com/clashcore26/clash-download/releases)
* [v0.20.39](https://github.com/clashcore26/clash-download/releases/tag/v0.20.39)

---

## 📌 Summary

Clash for Windows 的实际使用并不复杂。

对于刚开始使用的用户，优先掌握：

```text
下载安装
↓
导入配置
↓
选择 Profiles
↓
选择 Proxy Group
↓
开启 System Proxy
↓
测试网络
```

之后再逐步学习：

```text
Rules
↓
DNS
↓
TUN
↓
日志分析
↓
网络故障排查
```

这样可以避免一开始就修改大量高级参数，也更容易定位出现问题的具体环节。

本页面会随着仓库文档继续整理和更新。
