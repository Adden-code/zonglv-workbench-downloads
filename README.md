# 综履材料审核工作台：完整Windows下载

这里仅发布演示程序安装包，不是源码仓库。请选择Release中的EXE或便携ZIP，不要使用页面上的“Code / Download ZIP”。

## 下载

- [0.1.3完整Windows x64安装包](https://github.com/Adden-code/zonglv-workbench-downloads/releases/download/windows-v0.1.3-20261105/ZonglvAuditWorkbench-Setup-0.1.3-windows-x64.exe)
- [0.1.3完整便携ZIP](https://github.com/Adden-code/zonglv-workbench-downloads/releases/download/windows-v0.1.3-20261105/ZonglvAuditWorkbench-Portable-0.1.3-windows-x64.zip)
- [单独JAR（需要Java 21）](https://github.com/Adden-code/zonglv-workbench-downloads/releases/download/windows-v0.1.3-20261105/workbench-0.1.3.jar)
- [版本页面、配置说明与校验文件](https://github.com/Adden-code/zonglv-workbench-downloads/releases/tag/windows-v0.1.3-20261105)

本版将SYSTEM-IDENTITY改为“可见主账号名称匹配＋归一后平台一致”；内部KOL ID、主页和发布链接不再充当身份硬门槛。次要账号保留但不参与归属，缺失/矛盾/角色未知/同名多行无法区分仍转人工。独立业务规则保持原语义；预检对KOL ID、主页地址的equals/gte配置作非阻断提醒，不静默改规则。

0.1.2的可疑URL隔离、平台别名和像素预算，以及0.1.1的重试/恢复均保留。账号来源、辅助信息、排除的次要账号可在节点与Excel中检查。升级先停止旧实例、备份数据；已完成结果不重写，评估本版请新建轮次。旧版Release保留。

这两个包都含完整工作台、Java 21运行环境和合成KOL材料，无需再安装Java、Python或Node。便携版必须完整解压，不能只运行取出的EXE。

## 使用

1. 安装后打开桌面/开始菜单的“综履材料审核工作台”；便携版双击其中的`ZonglvAuditWorkbench.exe`。
2. 按提示配置获批且兼容当前应用的多模态模型地址、名称和密钥。没有模型也可先查看页面，但不能执行真实读图审核。
3. 用`samples/KOL-synthetic-10.zip`做演示，或在页面下载合成样本；样本不是正式业务规则。

发布包不含个人密钥、历史审核数据和真实业务材料。新填密钥用当前Windows账号的DPAPI加密保存在本机，不上传到此仓库。默认用户数据位置为`%LOCALAPPDATA%\MSS\ZonglvAuditWorkbench`；卸载保留用户数据。

## 验证边界

本轮Java165项通过/2项可选跳过/0失败，前端93项通过；包含合成14项的主次账号、内部ID不同、平台真实差异和独立链接规则回归，以及预检提醒不阻断启动的检查。发行物11项、捆绑Java独立服务12项、无头原生启动器6项、原生目录校验6项通过。完整安装向导、模型设置交互和卸载GUI仍需在目标电脑按单位规范复核，不能用组件测试代替。

上述外部测试没有调用真实模型、验证内部网络接口或证明业务准确率/ROI；格式合法的URL仍可能是幻觉，不能因格式通过就认定真实。程序未作商业代码签名；若安全软件拦截，请由IT评估准入，不要关闭安全防护。Windows 10/11 x64，启动器需Windows内置.NET Framework 4.x。

安装器采用NSIS与zlib压缩，开源许可信息随包保留；Java运行环境的许可在`runtime/legal`。本演示按现状提供，不替代企业生产系统及其权限、数据治理和运维建设。
