---
title: "SQL Server Management Studio (SSMS) - 候选发布 | Microsoft Docs"
ms.custom: 
ms.date: 03/09/2017
ms.prod: sql-vnext
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a4561ad6-5cfc-4c22-91a8-cf880fcbf233
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b8f51fcaa75e4567db3f52722d528ae5474f2ef4
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-management-studio-ssms---release-candidate"></a>SQL Server Management Studio (SSMS) - 候选发布
欢迎使用最新版 SQL Server Management Studio 候选发布 (17.0 RC3)！  此 SQL Server Management Studio (SSMS) 候选发布包括对 [SQL Server vNext](https://msdn.microsoft.com/library/mt788653.aspx) 的支持。 

## <a name="download"></a>下载

SSMS 候选发布 17.0 RC3 可与[正式发布版本 &#40;16.x&#41;](../ssms/download-sql-server-management-studio-ssms.md) 并行使用，但不建议用于生产。 
  
![下载](../ssdt/media/download.png)[ 下载 SQL Server Management Studio 17.0 RC3](https://go.microsoft.com/fwlink/?linkid=844503)。  
![下载](../ssdt/media/download.png)[下载 SQL Server Management Studio 17.0 RC3 升级包](https://go.microsoft.com/fwlink/?linkid=844505)。  
  
## <a name="enhancements"></a>增强功能 

- 新升级包
    - 将旧版 17.x 安装升级到最新版本
    - 减小了下载大小
    - 请参阅下面的“已知问题”，了解有关将 RC2 升级到 RC3 的具体问题
- 图标更新
    - 最终敲定了一组 SSMS 17.0 图标更新
    - 新增了 SSMS 和探查器程序图标，用于区分 16.x 和 17.x 版本
- 演示模式
    - 新增了 3 个可通过快速启动 (Ctr-Q) 执行的任务
    - PresentOn - 打开演示模式
    - PresentEdit - 编辑演示模式的演示字号。  对查询编辑器使用“文本编辑器字体”。  对其他组件使用“环境字体”。
    - RestoreDefaultFonts - 还原默认设置。
    - **注意：**目前没有 *PresentOff* 命令。  请使用 *RestoreDefaultFonts* 关闭演示模式
- SQL PowerShell 模块 
    - 对一些 SMO 对象的“演示”（格式设置）进行了其他改进（例如，数据库现在显示大小和可用空间，表显示行计数和空间使用情况）
    - 对通过对象资源管理器的“启动 PowerShell”菜单调用的 PowerShell 命令提示符进行了着色
    - 向 AG cmdlet（New-SqlAvailabilityGroup、Join-SqlAvailabilityGroup 和 Set-SqlAvailabilityGroup cmdlet）添加了 -ClusterType 和 -RequiredCopiesToCommit 参数
    - 向 Add-SqlAzureAuthenticationContext cmdlet 添加了 -ActiveDirectoryAuthority 和 -AzureKeyVaultResourceId 参数
- Linux 上的 SQL Server
    - 全面改进和修复了日志传送
- Analysis Server DAX 查询编辑器新增了着色和 IntelliSense
- 新增了“添加唯一约束”模板
- Showplan
    - 在运行时间的属性窗口中显示线程最大值（而非总和）
    - 公开了新的内存授予操作符属性
    - 在实时查询统计信息中启用了“编辑查询”按钮 d - 支持交叉执行
- 从已注册的服务器资源管理器中删除了配置管理器
- 支持从 Azure Blob 存储中读取审核日志

## <a name="bug-fixes"></a>Bug 修复

- 解决了“连接到服务器”对话框未保留“其他连接参数”选项卡中指定的设置的问题。 [连接项](https://connect.microsoft.com/SQLServer/feedback/details/813973)
- 解决了没有为用户定义的表类型编写默认值的问题。 [连接项](https://connect.microsoft.com/SQLServer/feedback/details/3119027)
- 对索引中的上下文菜单进行了另一轮性能改进。 [连接项](https://connect.microsoft.com/SQLServer/feedback/details/3120783)
- 解决了将鼠标悬停在执行计划缺少的索引之上时，闪烁次数过多的问题。 [连接项](https://connect.microsoft.com/SQLServer/feedback/details/3118510)
- 解决了编写脚本时 SSMS 导致 DB 脱机的问题 [连接项](https://connect.microsoft.com/SQLServer/feedback/details/3118550)
- 对本地化（非英语）版本的 SSMS 进行了其他 UI 修复。
- 解决了定位 SQL 2016 SP1 标准版时没有“Always Encrypted 密钥”节点的问题。
- 始终加密
    - 定位 SQL 2016 RTM 标准版或任意 SQL 2014（及更低版本）服务器时，“Always Encrypted”菜单未正确启用
    - 解决了使用 CREATE OR ALTER 语法时 IntelliSense 报告错误的问题
    - 解决了当 CMK/CEK 包含应转义的字符（即用括号括住）时无法加密的问题
    - 当 SSMS 中发生内存不足异常时，用户会看到一个错误消息，建议其改用本机（64 位）PowerShell。
    - 解决了在用户使用资源组管理器订阅（而不是经典 Azure 订阅）时，AE 向导无法运行的问题
    - 解决了在用户对任何订阅都没有权限，或对任何订阅都没有 Azure Key Vault 时，AE 向导显示不正确错误消息的问题。
    - 解决了在有多个 AAD 的情况下，AE 向导中的 Azure Key Vault 登录页不显示 Azure 订阅的问题
    - 解决了 AE 向导中的 Azure Key Vault 登录页不显示用户有权读取的 Azure 订阅的问题
- 改进了 SSMS 安装页上的超链接对比度
- 解决了连接 SQL Server Express (2016 SP1) 时看不到 PolyBase 节点的问题
- 解决了 SSMS 无法将 Azure SQL 数据库的兼容性级别更改为 v140 的问题
- 改进了展开 Azure 数据库列表时的对象资源管理器性能 [连接项](https://connect.microsoft.com/SQLServer/feedback/details/3100675)
- 解决了对非关系服务器类型 (AS\RS\IS) 错误显示“查看 SQL Server 日志”上下文菜单项的问题 
- 解决了使用 SQL 身份验证查看 Analysis Services 分区查询的语法时看到登录失败消息的问题
- 解决了在 SSMS 中无法重命名预览 1400 兼容性级别 AS 表格模型的问题
- 解决了在模型保存失败后还原本地更改的极少数情况下，尝试在 AS 服务器上执行无效操作后可能看到“无法对模型执行操作”错误消息的问题
- 更正了 Analysis Services 同步数据库弹出式对话框中的错别字

## <a name="known-issues"></a>已知问题

- 从 RC2 升级到 RC3 
    - 无法访问 AS、RS 和 IS 菜单选项
    - “工具”菜单中缺少“探查器和数据库优化引擎顾问”
    - 解决方法：重新运行 SSMS 17.0 RC3 安装程序，然后选择“修复”
    
- Linux 上的 SQL 支持：
    - 即将推出的 SSMS 更新程序将支持“Linux 上的 SQL”本机路径
    - 目前，SSMS 中的一些方案可能无法按预期运行。 例如：
        - “备份数据库”窗体中显示的路径如下：C:\var\opt\.。 （而不是本机 Linux 路径）。
        - 单击“备份数据库”向导上的“内容”按钮会导致错误发生。
    
## <a name="feedback"></a>反馈  
  
![需要帮助](../ssms/media/needhelp_person_icon.png) [SQL 客户端工具论坛](https://social.msdn.microsoft.com/Forums/en-US/home?forum=sqltools) |  [在 Microsoft Connect 中记录问题或建议](https://connect.microsoft.com/SQLServer/Feedback)。  
  
## <a name="see-also"></a>另请参阅  
[SQL Server Management Studio 教程](../ssms/use-sql-server-management-studio.md)  
[SQL Server vNext 中的新增功能](https://msdn.microsoft.com/library/mt788653.aspx)

