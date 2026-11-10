# 综履材料审核工作台：完整Windows下载

这里仅发布演示程序安装包，不是源码仓库。请选择Release中的EXE或便携ZIP，不要使用页面上的“Code / Download ZIP”。

## 下载

- [0.1.9完整Windows x64安装包](https://github.com/Adden-code/zonglv-workbench-downloads/releases/download/windows-v0.1.9-20261110/ZonglvAuditWorkbench-Setup-0.1.9-windows-x64.exe)
- [0.1.9完整便携ZIP](https://github.com/Adden-code/zonglv-workbench-downloads/releases/download/windows-v0.1.9-20261110/ZonglvAuditWorkbench-Portable-0.1.9-windows-x64.zip)
- [单独JAR（需要Java 21）](https://github.com/Adden-code/zonglv-workbench-downloads/releases/download/windows-v0.1.9-20261110/workbench-0.1.9.jar)
- [版本页面、配置说明与校验文件](https://github.com/Adden-code/zonglv-workbench-downloads/releases/tag/windows-v0.1.9-20261110)

0.1.9新增请求体字节预算`AUDIT_MODEL_MAX_REQUEST_BYTES`，默认3500000十进制字节，独立于像素、Token和超时。先按JSON/UTF-8/base64保守估计，最终在SDK序列化后按实际body字节检查，超限本地阻止。根据用户网关实测选择3.5MB安全值，不把其约4.0至4.2MB阈值推广为所有平台通用事实。

优先把原4图批次按字节拆小，分类每批保留context及标注，字段只带本批来源；单批仍超限才等比降采样发送副本。原图不覆盖，PNG/JPEG格式保持、短边不低于min(原短边,512)，无法安全适配就局部降级，不丢图/跨图补字段。节点可看实际字节、预算、原/发尺寸/字节/哈希、派发状态及发送副本。缩小可能影响小字，拆批重复context也可能增加调用和Token，真实质量与成本需原环境复测。

空200 JSON/SSE的全零签名、空体或仅SSE结束标记独立记`empty_upstream_response`，沿原连接类退避，不误当JSON纠错；非空reasoning、非零usage（含嵌套明细）、工具和非null finish不冒充全零响应。缺usage不伪造为0，usage全0不等于未计费。用户已将此前剩余现象定位为网关大包问题，旧解释作为历史保留。

0.1.8的非空stop且JSON未闭合仍用compact/minimal提示；原字段/角色/来源/覆盖校验、默认初次＋2次重试、输出预算不变，不拼补答案或关闭模型隐藏思考。载荷策略`utf8-body-budget-v1-20261110`、流程`java-sliced-v1.11-payload-budget`进入配置/轮次/节点/缓存指纹；旧完成节点不重写，新效果请新建同包轮次验证。

0.1.7及更早能力保留：“抖音短视频→抖音”，原值保留；微博、视频号与抖音不混同。继续保留“小红书蒲公英→小红书”及显式`likes,comments,collect`（赞评藏）求和，旧赞评转和空参数默认不改，不按平台切换或缺证补0。

角色指南区分笔记作者/达人元数据、代理登录与来源水印；Logo作平台而非账号，同图同作品明确时合并发布者/资料卡重复观察，导航/推荐/热搜/评论不污染主体与指标。不按名字或清单期望猜测，unknown/冲突仍人工；没有新增角色模型调用。角色策略可在配置/节点/Excel检查。新恢复提示会增加少量输入Token，整体消耗和恢复率仍需同包测量；不承诺缩短或关闭模型内部隐藏思考。

模型content保留单一完整JSON对象去包装与严格校验/退避；多个对象、重复键、未闭合或截断不补写、不充当证据。失败诊断新增实际finish_reason/max_tokens，语法残缺不直接认定Token根因。输出预算`AUDIT_MODEL_MAX_TOKENS`默认8192不变，思考型模型建议在获批网关支持后显式试65536，读取超时独立设置；更高预算可能增加实际耗时/费用，不承诺消除全部截断。

移除代理层JSON/Token临时补丁后，从设置环境变量的同一终端启动新版；须先停止旧实例，避免复用旧进程。核对`/api/java/config`的`model.max_tokens`，新建同包轮次查看实际请求预算、JSON去包装/重试、平台与求和依据。调大预算不保证识别质量，`finish_reason=length`仍拒收；完整说明见Release附件`MODEL-CONFIG.md`。

延续0.1.5身份门：主账号名称唯一匹配、无平台冲突时，平台缺失不阻断SYSTEM-IDENTITY；缺平台的独立平台规则单独待人工，其他规则正常核对，不从清单补造平台。名称矛盾、角色不明、同名未消歧等护栏保留。

数值提示词明确要求纯阿拉伯数字及精确单位转换，如43万→430000，不改写账号ID和发布单号。Excel按原始列字母取值，支持HTTP(S)超链接目标和已保存公式缓存；不执行公式、不访问链接，缓存可能陈旧需确认已计算保存。读取节点及报告留存列映射、显示文字/缓存/公式和采用值，便于对照原表排查；无缓存普通公式、表头/规则公式和危险链接仍拒收。

交付件类型双向包含比较继续保留：如“视频”与“60s以上视频”可判类型一致，但不代表时长等额外要求已核实。其他字段及独立规则保持，semantic仍转人工，不自动改配置。

互动量本版不增加容差，差异仍按原规则FAIL/待人工裁量；百分比或绝对值及阈值须业务确认后再实现。

主次账号留存、非阻断规则预警、URL隔离、别名/像素预算和重试/恢复均保留。升级先停止旧实例、备份数据；已有模型设置不改，已完成结果不重写，评估本版请新建轮次。旧0.1.8及更早Release保留。个人工作台试验不代表IT正式建设进展或业务验收。

这两个包都含完整工作台、Java 21运行环境和合成KOL材料，无需再安装Java、Python或Node。便携版必须完整解压，不能只运行取出的EXE。

## 使用

1. 安装后打开桌面/开始菜单的“综履材料审核工作台”；便携版双击其中的`ZonglvAuditWorkbench.exe`。
2. 按提示配置获批且兼容当前应用的多模态模型地址、名称和密钥。没有模型也可先查看页面，但不能执行真实读图审核。
3. 用`samples/KOL-synthetic-10.zip`做演示，或在页面下载合成样本；样本不是正式业务规则。

发布包不含个人密钥、历史审核数据和真实业务材料。新填密钥用当前Windows账号的DPAPI加密保存在本机，不上传到此仓库。默认用户数据位置为`%LOCALAPPDATA%\MSS\ZonglvAuditWorkbench`；卸载保留用户数据。

## 验证边界

本轮Java254项通过/2项可选跳过/0失败，前端104项通过；新增24项覆盖实际UTF-8 body、base64预算、真实Spring客户端拆批、context/来源完整性、失败小批保留、空JSON/SSE/仅DONE及误判反例、PNG/JPEG副本、超长Unicode文本本地拒绝和大响应完整回放；原0.1.8变体/65536/角色/平台/规则护栏回归通过。合成14/7项固定响应链路、三轮韧性及1440/390浏览器检查通过。发行物11项、捆绑Java独立服务18项、无头原生启动器8项、原生目录校验6项通过。合成链路刻意保留1项差异和1项缺证，不把completed等同全通过。完整安装向导、模型设置交互和卸载GUI仍需在目标电脑按单位规范复核，不能用组件测试代替。

上述外部测试没有调用真实模型、验证内部网络接口或证明业务准确率/ROI；格式合法的URL仍可能是幻觉，不能因格式通过就认定真实。程序未作商业代码签名；若安全软件拦截，请由IT评估准入，不要关闭安全防护。Windows 10/11 x64，启动器需Windows内置.NET Framework 4.x。

安装器采用NSIS与zlib压缩，开源许可信息随包保留；Java运行环境的许可在`runtime/legal`。本演示按现状提供，不替代企业生产系统及其权限、数据治理和运维建设。
