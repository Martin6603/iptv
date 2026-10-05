# M-Team 规则已迁移

域名规则已迁移到独立仓库 **[Martin6603/rules-dat](https://github.com/Martin6603/rules-dat)**。本目录仅保留迁移说明，后续源数据、生成工具和订阅文件统一在新仓库管理。

原 `iptv/main/rules/m-team/generated/` 订阅地址已停用，请替换为下列新地址。

| 集合 | 主机数 | `.list` | `.mrs` | `.yaml` |
| --- | ---: | --- | --- | --- |
| 核心服务 | 24 | [core.list](https://raw.githubusercontent.com/Martin6603/rules-dat/main/rules/m-team/core.list) | [core.mrs](https://raw.githubusercontent.com/Martin6603/rules-dat/main/rules/m-team/core.mrs) | [core.yaml](https://raw.githubusercontent.com/Martin6603/rules-dat/main/rules/m-team/core.yaml) |
| 图片等依赖 | 36 | [dependencies.list](https://raw.githubusercontent.com/Martin6603/rules-dat/main/rules/m-team/dependencies.list) | [dependencies.mrs](https://raw.githubusercontent.com/Martin6603/rules-dat/main/rules/m-team/dependencies.mrs) | [dependencies.yaml](https://raw.githubusercontent.com/Martin6603/rules-dat/main/rules/m-team/dependencies.yaml) |
| 合并集 | 60 | [m-team.list](https://raw.githubusercontent.com/Martin6603/rules-dat/main/rules/m-team/m-team.list) | [m-team.mrs](https://raw.githubusercontent.com/Martin6603/rules-dat/main/rules/m-team/m-team.mrs) | [m-team.yaml](https://raw.githubusercontent.com/Martin6603/rules-dat/main/rules/m-team/m-team.yaml) |

三种格式对应同一组精确主机名，均为 `behavior: domain`；provider 的 `format` 分别为 `text`、`mrs`、`yaml`。使用方式、来源和维护说明见[新仓库首页](https://github.com/Martin6603/rules-dat)。

迁移前的文件仍可通过[本仓库历史提交](https://github.com/Martin6603/iptv/tree/05974a97322f48951ca2cdbcfee2b9bdaa90cf3c/rules/m-team)查看和恢复。
