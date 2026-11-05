# 综履材料审核工作台：完整Windows下载

这里仅发布演示程序安装包，不是源码仓库。请选择Release中的EXE或便携ZIP，不要使用页面上的“Code / Download ZIP”。

## 下载

- [0.1.2完整Windows x64安装包](https://github.com/Adden-code/zonglv-workbench-downloads/releases/download/windows-v0.1.2-20261105/ZonglvAuditWorkbench-Setup-0.1.2-windows-x64.exe)
- [0.1.2完整便携ZIP](https://github.com/Adden-code/zonglv-workbench-downloads/releases/download/windows-v0.1.2-20261105/ZonglvAuditWorkbench-Portable-0.1.2-windows-x64.zip)
- [单独JAR（需要Java 21）](https://github.com/Adden-code/zonglv-workbench-downloads/releases/download/windows-v0.1.2-20261105/workbench-0.1.2.jar)
- [版本页面、配置说明与校验文件](https://github.com/Adden-code/zonglv-workbench-downloads/releases/tag/windows-v0.1.2-20261105)

本版在0.1.1重试/恢复基础上增加可疑URL隔离、平台别名归一、同名多行发布消歧、可配置单图/整份累计像素预算。原始读取值、归一依据和隔离原因留存可查；不确定证据仍转人工。默认单图40M/整份累计240M像素，详见随包MODEL-CONFIG.md。旧版Release保留。

这两个包都含完整工作台、Java 21运行环境和合成KOL材料，无需再安装Java、Python或Node。便携版必须完整解压，不能只运行取出的EXE。

## 使用

1. 安装后打开桌面/开始菜单的“综履材料审核工作台”；便携版双击其中的`ZonglvAuditWorkbench.exe`。
2. 按提示配置获批且兼容当前应用的多模态模型地址、名称和密钥。没有模型也可先查看页面，但不能执行真实读图审核。
3. 用`samples/KOL-synthetic-10.zip`做演示，或在页面下载合成样本；样本不是正式业务规则。

发布包不含个人密钥、历史审核数据和真实业务材料。新填密钥用当前Windows账号的DPAPI加密保存在本机，不上传到此仓库。默认用户数据位置为`%LOCALAPPDATA%\MSS\ZonglvAuditWorkbench`；卸载保留用户数据。

## 验证边界

已完成Java145项通过/2项可选跳过、前端90项通过，合成14项/6规则连续3轮故障注入完成、失败节点恢复、六页同名发布消歧及字段隔离检查。发行物11项、捆绑Java独立服务11项、无头原生启动器6项、原生目录校验6项通过。完整安装向导、模型设置交互和卸载GUI仍需在目标电脑按单位规范复核，不能用组件测试代替。

上述外部测试没有调用真实模型、验证内部网络接口或证明业务准确率/ROI；格式合法的URL仍可能是幻觉，不能因格式通过就认定真实。程序未作商业代码签名；若安全软件拦截，请由IT评估准入，不要关闭安全防护。Windows 10/11 x64，启动器需Windows内置.NET Framework 4.x。

安装器采用NSIS与zlib压缩，开源许可信息随包保留；Java运行环境的许可在`runtime/legal`。本演示按现状提供，不替代企业生产系统及其权限、数据治理和运维建设。
