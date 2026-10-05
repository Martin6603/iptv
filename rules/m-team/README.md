# M-Team 域名集

根据 2026-10-05 的实际 Chrome 浏览记录整理，格式参照 MetaCubeX `meta-rules-dat` 的 domain 规则集合。数据来源为 M-Team 主要页面、控制台服务选项、公开导航页、工单页和官方 Wiki。

本次记录 **79 个主机名**：**24 个核心服务**、**36 个图片等依赖**、**19 个资料外链或文档示例**。订阅合并集包含前两组，共 **60 个精确主机名**。这是首次采集版本，后续页面或历史帖子仍可能出现新的域名。

## 文件和订阅

| 集合 | 数量 | YAML 订阅 | Text 订阅 |
| --- | ---: | --- | --- |
| 核心服务 | 24 | [core.yaml](https://raw.githubusercontent.com/Martin6603/iptv/main/rules/m-team/generated/core.yaml) | [core.list](https://raw.githubusercontent.com/Martin6603/iptv/main/rules/m-team/generated/core.list) |
| 图片等依赖 | 36 | [dependencies.yaml](https://raw.githubusercontent.com/Martin6603/iptv/main/rules/m-team/generated/dependencies.yaml) | [dependencies.list](https://raw.githubusercontent.com/Martin6603/iptv/main/rules/m-team/generated/dependencies.list) |
| 合并集 | 60 | [m-team.yaml](https://raw.githubusercontent.com/Martin6603/iptv/main/rules/m-team/generated/m-team.yaml) | [m-team.list](https://raw.githubusercontent.com/Martin6603/iptv/main/rules/m-team/generated/m-team.list) |

- [DOMAINS.md](DOMAINS.md)：按用途分组的全部主机名和来源。
- [domains.json](domains.json)：可维护源数据，包含证据类型、页面路径和纳入规则的标记。
- [generated/](generated/)：从源数据生成的规则；`.txt` 与同组 `.list` 内容相同。
- [scripts/build.py](scripts/build.py)：仅依赖 Python 标准库的生成和一致性检查工具。

YAML 使用 `payload` 数组，Text 每行一个域名，均对应 `behavior: domain`。全部条目采用精确主机名，不扩展整个第三方根域；例如 `api.gateway996.com` 只匹配这个主机。格式依据：[MetaCubeX 规则集合内容说明](https://wiki.metacubex.one/config/rule-providers/content/)。

Mihomo YAML provider 示例（合并进已有配置）：

```yaml
rule-providers:
  m-team:
    type: http
    behavior: domain
    format: yaml
    url: https://raw.githubusercontent.com/Martin6603/iptv/main/rules/m-team/generated/m-team.yaml
    path: ./ruleset/m-team.yaml
    interval: 86400
```

随后在已有 `rules` 中按需要使用 `RULE-SET,m-team,你的策略组`，并替换为实际策略名称。选择 Text 订阅时，把 `format` 改成 `text`，同时使用对应 `.list` 地址。文件本身不指定直连或代理策略。

## 本次采集的关键服务

| 用途 | 观察到的主机名 |
| --- | --- |
| 桌面、备用和移动入口 | `kp.m-team.cc`、`zp.m-team.io`、`ob.m-team.cc`、`h5.m-team.cc`、`h5.m-team.io` |
| API | `api.m-team.cc`、`api.m-team.io`、`api2.m-team.cc` |
| 静态和站内图片 | `static.m-team.cc`、`img.m-team.cc` |
| 控制台种子下载选项 | `bt1.manfuz.co`、`fr1.halomt.com`、`hs1.holysalt.org` |
| 控制台 Tracker 选项 | `tracker.m-team.cc`、`tra1.m-team.cc`、`tracker.m-team.io`、`tra1.m-team.io`、`tra99.manfuz.co` |
| 控制台 RSS 选项 | `rss.m-team.cc`、`rss.m-team.io` |
| 官方说明和支持 | `wiki.m-team.cc`、`ticket.m-team.io` |
| 图片重定向网关 | `api.gateway996.com` |

核心集包含 M-Team 命名空间内的服务，以及控制台明确提供的下载和 Tracker 端点。控制台提供的其他域名按服务角色归类，不据此断言其法律归属。第三方依赖集包含共享图床、封面 CDN、移动版字体样式，以及图片网关 `uri` 参数引用的上游主机。为其他网站提供服务的同一精确主机也会匹配依赖规则；需要较窄范围时选用核心集。

资料网站、Telegram、软件页脚、Wiki 引用的工具等仅作为外链记录。`tracker.abcdef.com` 是 Wiki 配置示例占位符，未加入任何规则。没有猜测未观察到的子域名，也没有照搬历史公共规则中的其他域名。

官方网址入口证据：[官方 Wiki 入口说明](https://wiki.m-team.cc/zh-tw/siteurl)。控制台选项来自已登录站点的个人设定页，仅展开查看，没有选择新值或保存设置。

## 与图片加载错误的关系

本次用户控制台错误指向 `api.gateway996.com`，提示请求访问 `local` 地址空间被拒绝。将域名加入普通分流规则本身不会修复 DNS 返回本地地址或 Fake-IP 的问题。

若已有 Mihomo DNS 配置使用 `fake-ip-filter-mode: blacklist`，可先把精确主机 `api.gateway996.com` 合并进现有 `fake-ip-filter`，让它不返回 Fake-IP。应保留原有过滤项及其他 DNS 设置；`whitelist` 或 `rule` 模式需按各自语义调整。需要更广范围时可参考 [generated/fake-ip-filter.yaml](generated/fake-ip-filter.yaml)，其中列出合并集，只作为合并示例。依据：[Mihomo DNS 过滤说明](https://wiki.metacubex.one/config/dns/#fake-ip-filter)。

这份规则集没有修改用户本机 DNS、浏览器权限或网络设置，也不保证仅靠过滤项就能解决所有图片加载失败。

## 来源与覆盖范围

本次有 40 次页面或页面状态采集，脱敏后对应 30 个不同页面路径，覆盖首页、电影、电视、音乐、综合分类、游戏、电子书、软件、成人分类、一个详情页、片单列表、论坛、求种、候选、字幕、制作组、展示、上传页、活动和支持页面，以及 Wiki 的入口、下载规则、FAQ、Tracker 故障和 IP 说明。

证据保存在 `domains.json`：`page` 表示实际页面地址；`link`、`image`、`script` 等来自 DOM；`visible_domain` 来自可见服务选项；`observed_*` 来自浏览器已观察的资源清单；`nested_uri` 表示图片参数中的上游主机，`nested_imdb`／`nested_douban` 表示资料目标链接。

浏览器资源清单可能保留 SPA 较早请求，故 `observed_*` 不能证明每个页面都重新请求了该域名。每个主机和证据类型仅保留首次记录，重复记录已归并；采集页面及状态单独列出。图片上游参数也不等于浏览器直接连接过上游。备用入口部分只查看登录页或链接；没有穷尽所有历史种子、帖子、用户图床，也没有探测 Tracker 的可用性。

保存的信息只含主机名和脱敏来源路径，不包含完整图片签名 URL、passkey、账户信息、Cookie 或具体详情页编号。

## 维护

1. 在实际页面中确认新域名，记录用途及脱敏来源；区分页面请求、上游参数、资料外链和占位示例。
2. 修改 `domains.json`，更新采集日期、时区、覆盖范围及 `include_in_core`／`include_in_dependencies` 标记。两组不得重叠，外链不进入规则。
3. 在本目录执行 `python scripts/build.py`，然后执行 `python scripts/build.py --check`。
4. 一并提交源数据、明细说明和生成文件；数量或范围发生变化时更新本说明。

本目录独立于仓库原有 IPTV 数据和程序；生成器只写入本目录的 `generated/`。
