# Loon 分组与分流配置

[一键导入配置](https://www.nsloon.com/openloon/import?sub=https%3A%2F%2Fraw.githubusercontent.com%2Fnullspacecn%2Fopenclash-rules%2Fmain%2FLoon%2FPerfect-Rules-Loon.conf) · [配置原文](https://raw.githubusercontent.com/nullspacecn/openclash-rules/main/Loon/Perfect-Rules-Loon.conf)

## 初次使用

1. 先导出备份当前 Loon 配置。一键链接导入的是完整配置模板；不保证自动合并或保留当前节点、插件和 MitM 设置。
2. 在 iPhone Safari 打开一键链接，导入配置，选择规则模式。
3. 在节点订阅中编辑 `机场订阅`：填入自己的 **Loon 原生或 Loon 可直接解析的节点订阅地址**，将禁用改为启用，更新订阅。不要把私人订阅地址提交到 GitHub。机场只有 Clash YAML 时，先在机场获取 Loon 链接；此模板不自带订阅转换器。
4. 检查低倍率筛选是否有节点，默认代理及 YouTube 选中低倍率自动；Emby 组可独立选具体节点或地区。
5. 建议首次保存为本地配置使用；远程完整配置更新可能覆盖本地填写的订阅，需要保留本地订阅段。

## 已有 Loon 节点与插件

打开 `Merge-Sections.txt`，将现有订阅别名改为 `机场订阅`，或修改片段的订阅别名；按段合并筛选器、策略组、本地规则和远程规则。保留现有 General、Proxy、Remote Proxy、插件和 MitM。多机场需在每个 NameRegex 的来源列表中列出各订阅别名。单独导入规则订阅不会创建分组，不能替代完整配置。

## 保留的行为

- 共 23 个策略组，保留原业务顺序、地区单字筛选和独立手选节点入口。
- 低倍率只匹配名称明确标记 `0.01x / 0.1x` 或 `×` 的节点；未知倍率不加入低倍率组。倍率来源是节点名称，不能验证实际计费。
- `younoyes.com` 及全部子域名均交给 Emby 组。DERP 域名 `derp.sa.930702.xyz` 直连且列入 real-ip。
- Tailscale 域名、私网地址及 UDP 端口规则保留；GitHub 使用独立组。
- 7 个 Smart 组转换为测速自动组，300 秒间隔、50 毫秒切换容差。Loon 不采用 Mihomo Smart 的历史权重和 LightGBM 字段。

## 转换边界和更新

- Loon 的域名、IP 与规则来源匹配优先级和 OpenClash 不完全相同；本地特殊域名优先。首次使用检查 Loon 请求记录中的策略。
- `empty-fallback`、`expected-status`、`lazy` 等 Mihomo 参数不复制。手选组提供 REJECT 选项；自动组没有加入全倍率或 DIRECT 兜底。Loon 空筛选器／自动组的实际行为尚未本机验证，低倍率为空时先选择 REJECT，或手动选择确定倍率的节点；不能据此承诺与 OpenClash 空组拒绝完全等价。
- GeoSite 转为 MetaCubeX 的同分类纯域名文本快照；覆盖范围取决于该域名导出，不保证与设备原 geosite.dat 的关键字、正则或版本一致。CN 使用该项目所采用的 ChinaMax 来源的 Loon 规则订阅。
- 本仓库 `rules/` 是 2026-10-06 的转换快照；刷新 Loon 会获取本仓库当前版本，不会自动重新展开上游 GeoSite。ChinaMax 是直接引用上游，可随上游更新。
- 已进行格式、分组引用、低倍率筛选和规则转换静态检查；尚未在 iPhone Loon 中启动验证。建议 Loon 3.2.3 或更新版本。

## 规则来源与格式依据

原配置：[Perfect-Rules](https://github.com/n0de-sudo/Perfect-Rules)。域名分类：[MetaCubeX/meta-rules-dat](https://github.com/MetaCubeX/meta-rules-dat)。国内规则：[ChinaMax](https://github.com/blackmatrix7/ios_rule_script/tree/master/rule/Loon/ChinaMax)。保留上游项目归属；本转换不重新授予上游规则许可。

[Loon 官方格式样例](https://github.com/Loon0x00/LoonExampleConfig/blob/master/example.conf)、[策略组](https://nsloon.app/en/docs/Policy/policygroup/)、[规则优先级](https://nsloon.app/en/docs/Rule/)、[一键导入](https://nsloon.app/en/docs/Scheme/)。
