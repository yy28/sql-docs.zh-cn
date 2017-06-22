---
title: "以前的 SQL Server Management Studio 版本 | Microsoft Docs"
ms.custom: 
ms.date: 01/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 87f593c3-8b76-4c12-963a-31d35f2fb294
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 0927784589c1f7227b432ff49f81f29de20083ec
ms.openlocfilehash: 200753bf64d92043171788852227c6199b64711d
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="previous-sql-server-management-studio-releases"></a>以前的 SQL Server Management Studio 版本
  
提供以下以前版本的 SQL Server Management Studio。
   
## <a name="downloadssdtmediadownloadpng-sql-server-management-studio-1653-releasehttpgomicrosoftcomfwlinklinkid840946"></a>![下载](../ssdt/media/download.png) [SQL Server Management Studio 16.5.3 版本](http://go.microsoft.com/fwlink/?LinkID=840946)

**版本信息**  
  
*此版本的 SSMS 使用 Visual Studio 2015 独立 shell。*  
版本号：16.5.3  
此版本的内部版本号为：13.0.16106.4

## <a name="changelog"></a>更改日志  

16.5.3

此版本已解决以下问题：

* 解决了 SSMS 16.5.2 中引入的问题，即当表具有多个稀疏列时，导致“表”节点扩展。

* 用户可以部署包含 OData 连接管理器的 SSIS 包，这些包连接到 SSIS 目录的 Microsoft Dynamics AX / CRM Online 资源。 有关详细信息，请参阅 [OData 连接管理器](https://msdn.microsoft.com/library/dn584133.aspx)。

* 为现有表配置“始终加密”功能失败，在不相关的对象上出错。 [连接 ID 3103181](https://connect.microsoft.com/SQLServer/feedback/details/3103181/setting-up-always-encrypted-on-an-existing-table-fails-with-errors-on-unrelated-objects)

* 为现有数据库配置“始终加密”功能时，多个架构无法正常运行。 [连接 ID 3109591](https://connect.microsoft.com/SQLServer/feedback/details/3109591/sql-server-2016-always-encrypted-against-existing-database-with-multiple-schemas-doesnt-work)

* 由于数据库包含引用系统视图的视图，“始终加密、已加密列”向导失败。 [连接 ID 3111925](https://connect.microsoft.com/SQLServer/feedback/details/3111925/sql-server-2016-always-encrypted-encrypted-column-wizard-failed-task-failed-due-to-following-error-cannot-save-package-to-file-the-model-has-build-blocking-errors)

* 使用“始终加密”功能进行加密时，错误处理加密后刷新模块出现错误。

* “打开最近的文件”菜单不显示最近保存的文件。 [连接 ID 3113288](https://connect.microsoft.com/SQLServer/feedback/details/3113288/ssms-2016-open-recent-menu-doesnt-show-recently-saved-files)

* 右键单击表的索引（通过远程 (Internet) 连接）时，SSMS 运行缓慢。 [连接 ID 3114074](https://connect.microsoft.com/SQLServer/feedback/details/3114074/ssms-slow-when-right-clicking-an-index-for-a-table-over-a-remote-internet-connection)
 
* 解决了 SQL 设计器滚动条的问题。 [连接 ID 3114856](http://connect.microsoft.com/SQLServer/feedback/details/3114856/bug-in-scrollbar-on-sql-desginer-in-ssms-2016)

* 表的上下文菜单暂时挂起 
 
* SSMS 偶尔在活动监视器中引发异常和崩溃。 [连接 ID 697527](https://connect.microsoft.com/SQLServer/feedback/details/697527/)

* SSMS 2016 崩溃，显示错误“由于在 IP 71AF8579 (71AE0000) 的 .NET 运行时出现内部错误，进程终止，退出代码 80131506”



## <a name="downloadssdtmediadownloadpng-sql-server-management-studio-165-releasehttpgomicrosoftcomfwlinklinkid832812"></a>![下载](../ssdt/media/download.png) [SQL Server Management Studio 16.5 版](http://go.microsoft.com/fwlink/?LinkID=832812)

**版本信息**  
  
*此版 SSMS 使用 Visual Studio 2015 独立 Shell。*  
发行版号：16.5  
此发行版的版本号为：13.0.16000.28

**此版本的已知问题**  

1. 在进行检查约束时 Invoke-Sqlcmd 会错误插入多个行。 [Microsoft Connect 项目：811560](https://connect.microsoft.com/SQLServer/feedback/details/811560)

2. 创建可用性组时非 ENU 语言版本无法完全使用。

3. 单击查询计划 XML 时不能打开相应 SSMS UI。

**更改日志**

* 修复了当单击具有包含“;:”的表名称的数据库时可能发生故障的问题。
* 修复了在“AS 表格数据库属性”窗口中对“模型”页所做的更改将编写原始定义的脚本的问题。 
[Microsoft Connect 项：3080744](https://connect.microsoft.com/SQLServer/feedback/details/3080744) 
* 修复了将临时文件添加到“最近使用过的文件”列表的问题。  
[Microsoft Connect 项：2558789](https://connect.microsoft.com/SQLServer/feedback/details/2558789)
* 修复了在对象资源管理器树中对用户表节点禁用“管理压缩”菜单项的问题。  
[Microsoft Connect 项：3104616](https://connect.microsoft.com/SQLServer/feedback/details/3104616)

* 修复了用户不能设置对象资源管理器、已注册的服务器资源管理器、模板资源管理器以及对象资源管理器详细信息的字体大小的问题。 资源管理器的字体将会使用“环境”字体。  
[Microsoft Connect 项：691432](https://connect.microsoft.com/SQLServer/feedback/details/691432)

* 修复了在连接丢失时 SSMS 始终重新连接到默认数据库的问题。  
[Microsoft Connect 项：3102337](https://connect.microsoft.com/SQLServer/feedback/details/3102337)

* 修复了策略管理和查询编辑器窗口中许多高 DPI 的问题，包括执行计划图标。

* 修复了缺少为扩展的事件配置字体和颜色的选项问题。

* 修复了在关闭应用程序或 SSMS 尝试显示错误对话框时发生故障的问题。


   
## <a name="downloadssdtmediadownloadpng-sql-server-management-studio-1641-september-2016-releasehttpgomicrosoftcomfwlinklinkid828615"></a>![下载](../ssdt/media/download.png) [SQL Server Management Studio 16.4.1（2016 年 9 月）版本](http://go.microsoft.com/fwlink/?LinkID=828615)

**版本信息**  
  
*此版本的 SSMS 使用 Visual Studio 2015 独立 shell。*  
版本号：16.4.1  
此版本的版本号为：13.0.15900.1
  
**此版本的已知问题**  

1. **仅单个 Azure Active Directory 帐户可以使用 Active Directory 通用身份验证为 SSMS 实例登录。**  
    此限制仅限于 Active Directory 通用身份验证 - 你可以使用 Active Directory 密码身份验证、Active Directory 集成身份验证或 SQL Server 身份验证登录不同的服务器。
    
    作为一种解决方法，你可以使用 SSMS 的其他实例以另一个 Azure Active Directory 帐户身份登录。 
    
2. **SSMS 中的数据层应用程序框架 (DacFx) 命令和架构设计器不支持 Active Directory 通用身份验证。**  
    使用 SSMS 中的 DacFx 架构设计器的命令（例如，导入和导出）目前不支持 Active Directory 通用身份验证。
    
    作为一种解决方法，你可以使用 SSMS 中提供的其他形式的身份验证 - Active Directory 密码身份验证、Active Directory 集成身份验证或 SQL Server 身份验证。

3. **SSMS 只能连接到 SQL Server 2016 Integrated Services (SSIS 2016) 实例。**  
    SQL Server Integration Services 存在已知的兼容性限制，会阻止与早期版本的连接。
    
    作为此问题的一种解决方法，你可以使用 [匹配你的 SSIS 实例的 SSMS 版本](../ssms/previous-sql-server-management-studio-releases.md)连接到 SQL Server Integration Service 实例 
  
4. **SSMS 不会保存 SQL Server 2008 R2 和较早版本的 SQL Server 的维护计划。**  
    我们希望此已知限制在以后得以解决。 与此同时，你可以使用 [SSMS 2014 版本](../ssms/previous-sql-server-management-studio-releases.md) 来保存维护计划。  
    
5. **非英语版 SSMS 安装可能需要安装其他安全包。**  
如果安装在以下系统中，则非英语本地化版本的 SSMS [需要 KB 2862966 安全更新程序包](https://support.microsoft.com/en-us/kb/2862966) ：Windows 8、Windows 7、Windows Server 2012 和 Windows Server 2008 R2。
  
6. **如果客户端计算机上未安装 SQL Server，则 SQL Server 配置管理器将无法启动**  
    如果你未在自己的客户端计算机上安装 SQL Server，并启动了 SQL Server 配置管理器，将看到以下错误：   
     `Cannot connect to WMI provider. You do not have permission or the server is unreachable. Note that you can only manage SQL Server 2005 and later servers with SQL Server Configuration Manager. Invalid namespace \[0x8004100e]`、   
   
     * 如果你已将 SQL Server 实例添加到 SSMS 中的“已注册的服务器”列表，请执行以下操作：  
        1. 导航至 SSMS 中的“已注册服务器”视图。  
        2. 右键单击你想要配置的 SQL Server 实例。  
        3. 从右键菜单中 选择“SQL Server 配置管理器...”。    
          
      * 如果你尚未将 SQL Server 实例添加到 SSMS 中的“已注册的服务器”列表，请执行以下操作：  
        1. 以管理员身份打开命令提示符。  
        2. 使用下列命令运行 Mofcomp 工具：  
    `mofcomp "%programfiles(x86)%\Microsoft SQL Server\130\Shared\sqlmgmproviderxpsp2up.mof"`  
        3. 在运行 Mofcomp 工具后，运行下列命令来重启 WMI 服务以使更改生效：  
        `net stop "Windows Management Instrumentation"`  
        `net start “Windows Management Instrumentation”`  

 
**更改日志** 

*  解决了尝试更改/修改存储过程失败的问题：  
[Microsoft Connect 项目 #3103831](https://connect.microsoft.com/SQLServer/feedback/details/3103831)

* 新增了通过 PowerShell 来查看和写入数据的“Read-SqlTableData”、“Read-SqlViewData”和“Write-SqlTableData”cmdlet。  
[Trello Read-SqlTableData 卡](https://trello.com/c/FXVUNJ8x/131-read-sqltabledata)  
[Microsoft Connect 项目 #2685363](https://connect.microsoft.com/SQLServer/feedback/details/2685363)
    
* 新增了用于通过 PowerShell 来启用新登录管理方案的“Add-SqlLogin”cmdlet。  
[Microsoft Connect 项目 #2588952](https://connect.microsoft.com/SQLServer/feedback/details/2588952)
    
*  为连接到各种国内云的用户改进了支持和可用性。
    
*  解决了引发内存不足异常的问题。  
[Microsoft Connect 项目 #3062914](https://connect.microsoft.com/SQLServer/feedback/details/3062914)  
[Microsoft Connect 项目 #3074856](https://connect.microsoft.com/SQLServer/feedback/details/3074856)
    
*  解决了按架构筛选不是有效筛选选项的问题。  
[Microsoft Connect 项目 #3058105](https://connect.microsoft.com/SQLServer/feedback/details/3058105)  
[Microsoft Connect 项目 #3101136](https://connect.microsoft.com/SQLServer/feedback/details/3101136)
    
*  解决了拉伸数据库监视器窗口不可访问的问题。
    
*  解决了 F1 帮助始终打开联机内容的问题。 用户现可选择通过“帮助”菜单中“设置帮助首选项”来实现联机帮助还是脱机帮助。   
[Microsoft Connect 项目 #2826366](https://connect.microsoft.com/SQLServer/feedback/details/2826366)
    
*  解决了以下问题：删除 1200 级别 Analysis Services 表格模型不会删除用于脚本编写的密码，即使服务器版本有密码 [客户端模型对象在脚本编写前现已同步]。
    
*  解决了“选择前 N 行”选项生成了 TOP 运算符的已弃用语法的问题。  
[Microsoft Connect 项目 #3065435](https://connect.microsoft.com/SQLServer/feedback/details/3065435)
    
*  解决了整个 SSMS 的布局问题，包括登录属性页和高级查询执行选项。   
[Microsoft Connect 项目 #3058199](https://connect.microsoft.com/SQLServer/feedback/details/3058199)  
[Microsoft Connect 项目 #3079122](https://connect.microsoft.com/SQLServer/feedback/details/3058199)  
[Microsoft Connect 项目 #3071384](https://connect.microsoft.com/SQLServer/feedback/details/3071384)
    
*  解决了只要用户打开新查询窗口即自动创建解决方案的问题。   
[Microsoft Connect 项目 #2924667](https://connect.microsoft.com/SQLServer/feedback/details/2924667)    
[Microsoft Connect 项目 #2917742](https://connect.microsoft.com/SQLServer/feedback/details/2917742)   
[Microsoft Connect 项目 #2612635](https://connect.microsoft.com/SQLServer/feedback/details/2612635)
    
*  解决了临时表位于系统数据库时无法在对象资源管理器中展开的问题。  
[Microsoft Connect 项目 #2551649](https://connect.microsoft.com/SQLServer/feedback/details/2551649)
    
*  解决了 SSMS 执行批处理后运行 SELECT @@trancount 查询的问题。    
[Microsoft Connect 项目 #3042364](https://connect.microsoft.com/SQLServer/feedback/details/3042364)
    
*  解决了 Analysis Services 中从服务器属性页创建脚本产生隐藏连接对话框的问题。
    
*  解决了按 Ctrl+Q 不会选择“快速启动”工具栏的问题。
    
*  解决了使用“服务器属性”对话框更改数据库最大大小对超过 2 TB 数据库不起作用的问题。  
[Microsoft Connect 项目 #1231091](https://connect.microsoft.com/SQLServer/feedback/details/1231091)
    
*  解决了“还原数据库”向导不接受含前导空格的文件名的问题：   
[Microsoft Connect 项目 #2395147](https://connect.microsoft.com/SQLServer/feedback/details/2395147)

*  解决了“还原数据库”向导不接受含前导空格的文件名的问题：   
[Microsoft Connect 项目 #2395147](https://connect.microsoft.com/SQLServer/feedback/details/2395147)



## <a name="downloadssdtmediadownloadpng-sql-server-management-studio-163-august-2016-releasehttpgomicrosoftcomfwlinklinkid824938"></a>![下载](../ssdt/media/download.png) [SQL Server Management Studio 16.3（2016 年 8 月）版本](http://go.microsoft.com/fwlink/?LinkID=824938)
 2016 年 8 月 15 日 | 版本号：13.0.15700.28

**功能**  
1. 新增身份验证选项“Active Directory 通用身份验证”
2. 新增 SQL Server PowerShell 模块 cmdlet
3. 改进数据库引擎优化顾问 (DTA) 和扩展事件模板
4. 对 [SSMS 中的高分辨率显示器](https://blogs.msdn.microsoft.com/sqlreleaseservices/ssms-highdpi-support/)的测试版支持

[可在 SSMS 更改日志中获取有关功能的详细信息。](../ssms/sql-server-management-studio-changelog-ssms.md)

**已知问题**

以下是此 SQL Server Management Studio 版本的问题和限制：  

1. **仅单个 Azure Active Directory 帐户可以使用 Active Directory 通用身份验证为 SSMS 实例登录。**  
    此限制仅限于 Active Directory 通用身份验证 - 你可以使用 Active Directory 密码身份验证、Active Directory 集成身份验证或 SQL Server 身份验证登录不同的服务器。
    
    作为一种解决方法，你可以使用 SSMS 的其他实例以另一个 Azure Active Directory 帐户身份登录。 
    
2. **SSMS 中的数据层应用程序框架 (DacFx) 命令和架构设计器不支持 Active Directory 通用身份验证。**  
    使用 SSMS 中的 DacFx 架构设计器的命令（例如，导入和导出）目前不支持 Active Directory 通用身份验证。
    
    作为一种解决方法，你可以使用 SSMS 中提供的其他形式的身份验证 - Active Directory 密码身份验证、Active Directory 集成身份验证或 SQL Server 身份验证。

3. **SSMS 只能连接到 SQL Server 2016 Integrated Services (SSIS 2016) 实例。**  
    SQL Server Integration Services 存在已知的兼容性限制，会阻止与早期版本的连接。
    
    作为此问题的一种解决方法，你可以使用 [匹配你的 SSIS 实例的 SSMS 版本](../ssms/previous-sql-server-management-studio-releases.md)连接到 SQL Server Integration Service 实例 
  
4. **SSMS 不会保存 SQL Server 2008 R2 和较早版本的 SQL Server 的维护计划。**  
    我们希望此已知限制在以后得以解决。 与此同时，你可以使用 [SSMS 2014 版本](../ssms/previous-sql-server-management-studio-releases.md) 来保存维护计划。  
    
5. **非英语版 SSMS 安装可能需要安装其他安全包。**  
如果安装在以下系统中，则非英语本地化版本的 SSMS [需要 KB 2862966 安全更新程序包](https://support.microsoft.com/en-us/kb/2862966) ：Windows 8、Windows 7、Windows Server 2012 和 Windows Server 2008 R2。
  
6. **如果客户端计算机上未安装 SQL Server，则 SQL Server 配置管理器将无法启动**  
    如果你未在自己的客户端计算机上安装 SQL Server，并启动了 SQL Server 配置管理器，将看到以下错误：   
     `Cannot connect to WMI provider. You do not have permission or the server is unreachable. Note that you can only manage SQL Server 2005 and later servers with SQL Server Configuration Manager. Invalid namespace \[0x8004100e]`、   
   
     * 如果你已将 SQL Server 实例添加到 SSMS 中的“已注册的服务器”列表，请执行以下操作：  
        1. 导航至 SSMS 中的“已注册服务器”视图。  
        2. 右键单击你想要配置的 SQL Server 实例。  
        3. 从右键菜单中 选择“SQL Server 配置管理器...”。    
          
      * 如果你尚未将 SQL Server 实例添加到 SSMS 中的“已注册的服务器”列表，请执行以下操作：  
        1. 以管理员身份打开命令提示符。  
        2. 使用下列命令运行 Mofcomp 工具：  
    `mofcomp "%programfiles(x86)%\Microsoft SQL Server\130\Shared\sqlmgmproviderxpsp2up.mof"`  
        3. 在运行 Mofcomp 工具后，运行下列命令来重启 WMI 服务以使更改生效：  
        `net stop "Windows Management Instrumentation"`  
        `net start “Windows Management Instrumentation”`  


**修复程序**
1. 用于查看 SSMS 中已解密的 AlwaysEncrypted 大型对象 (LOB) 列的明文的 Bug 修复（Microsoft Connect 项目 #2413024）。
2. “始终加密”对话框中的 Bug 修复，可以修复在 Windows 视觉样式未启用（例如，启用高对比度显示器）时的故障。
3. “找不到方法”错误阻止连接到 SQL Server 实例的 Bug 修复。
4. 使用日期时间偏移创建分区函数时出现 SSMS 故障的 Bug 修复。
5. 用于删除对启动分布式重播管理工具 (DReplay.exe) 的 Microsoft .NET 3.5 要求的 Bug 修复。
6. Analysis Services 部署向导中的 Bug 修复，支持完全限定的服务器名称。
7. SSMS 中的 Bug 修复，可以使用 2016 兼容性模型显示 Analysis Services 表格模型中的分区（Microsoft Connect 项目 #2845053）。

[可在 SSMS 更改日志中获取有关修复的详细信息。](../ssms/sql-server-management-studio-changelog-ssms.md)
 
---
## <a name="downloadssdtmediadownloadpng-sql-server-management-studio-july-2016-hotfix-update-releasehttpgomicrosoftcomfwlinklinkid822301"></a>![下载](../ssdt/media/download.png) [SQL Server Management Studio 修补程序更新版本（2016 年 7 月）](http://go.microsoft.com/fwlink/?LinkID=822301)

2016 年 7 月 13 日 | 版本号：13.0.15600.2

**功能**  
1. 在 SSMS 中对 Azure SQL 数据仓库的支持。   
2. 对 SQL Server PowerShell 模块的重要更新。   
3. 显著改善了到 Azure SQL 数据库的连接时间。  
4. 改进了对“Analysis Services 进程”对话框中 SQL Server 2016（1200 兼容级别）表格数据库和对其他内容的支持。   

[可在 SSMS 更改日志中获取详细信息及更多功能。](../ssms/sql-server-management-studio-changelog-ssms.md)

**已知问题** 
1. **SSMS 7 月修补程序版本的安装程序显示为 SSMS 8 月版本。**
内部版本设置导致 7 月更新修补程序的安装程序页显示为 8 月。 但实际上此包是 SSMS 7 月版本修补程序。 
2. **安装“2016 年 7 月修补程序”版本后，SSMS 无法连接到 SQL Server 实例。**
我们发现有关最新 SSMS 更新程序的一个问题，即尝试连接到服务器导致出现下列错误消息： 
   ```
    "Method not found: 'Void Microsoft.SqlServer.Management.Common.SqlConnectionInfo.set_ApplicationIntent(System.String)'"
    ```
  
    此问题的修复程序将在下次发行的 SSMS 版本中提供。 作为此问题的解决方法，你可以在卸载后重新安装 SSMS。 有关详细信息，请 [访问有关此问题的 Microsoft Connect 线程](https://connect.microsoft.com/SQLServer/feedback/details/2925257/not-able-to-connect-to-sql-server-instances-after-installing-ssms-2016-july-update)。
    
3. **尝试选择 Azure 存储帐户时 SSMS 出现故障。**
如果尝试选择 Azure 存储帐户但不具备“经典”存储帐户，SSMS 7 月版本和 7 月修补程序版本会出现故障。
此问题的修复程序将在即将发布的 SSMS 版本中提供。 作为此问题的解决方法，你可以通过创建经典存储帐户或者通过 [使用 T-SQL 进行备份或还原](https://msdn.microsoft.com/library/jj720552(v=sql.120).aspx)将数据库备份/还原至 Azure 存储帐户。

4. **SSMS 将仅显示“备份/还原”向导中的“经典”Azure 存储帐户。**
如果你正在尝试使用“备份或还原”向导进行备份或还原，则 SSMS 7 月版本和 7 月修补程序版本仅显示新创建凭据的“经典”Azure 存储帐户。
此问题的修复程序将在即将发布的 SSMS 版本中提供。 作为此问题的解决方法，你可以 [使用 T-SQL 进行备份或还原](https://msdn.microsoft.com/library/jj720552(v=sql.120).aspx)，将数据库备份/还原至可用的 Azure“经典”存储帐户或者备份至“ARM-type”存储帐户。 

5. **非英语版 SSMS 安装可能需要安装其他安全包。**
如果安装在以下平台中，非英语本地化版本的 SSMS 需要 [KB 2862966 安全更新程序包](https://support.microsoft.com/en-us/kb/2862966) ：Windows 8、Windows 7、Windows Server 2012 和 Windows Server 2008 R2。
6. **SSMS 只能连接到 SQL Server 2016 Integrated Services (SSIS 2016) 实例。** SQL Server Integration Services 存在已知的兼容性限制，会阻止与早期版本的连接。
作为此问题的一种解决方法，你可以使用匹配你的 SSIS 实例的 SSMS 版本连接到 SQL Server Integration Service 实例。
7. **SSMS 不会保存 SQL Server 2008 R2 和较早版本的 SQL Server 的维护计划。** 我们正在努力修复此问题。 与此同时，你可以使用 SSMS 2014 以下的版本来保存维护计划。
8. **如果客户端计算机上未安装 SQL Server，则SQL Server 配置管理器将无法启动。** 如果你未在自己的客户端计算机上安装 SQL Server，并启动了 SQL Server 配置管理器，你将收到“无法连接到 WMI 提供程序”错误。 解决方法如下：
    * 以管理员身份打开命令提示符。
    * 使用下列命令运行 Mofcomp 工具：  
      mofcomp "%programfiles(x86)%\Microsoft SQL Server\130\Shared\sqlmgmproviderxpsp2up.mof"
    * 在运行 Mofcomp 工具后，运行下列命令来重启 WMI 服务以使更改生效：  
       net stop "Windows Management Instrumentation"  
       net start "Windows Management Instrumentation"

**修复程序**  
1. SSMS 查询设计器中的 Bug 修复，如果用户对表没有 SELECT 权限，则允许将表添加到设计器中。
2. 用于为“TRY_CAST()”和“TRY_CONVERT()”函数添加 IntelliSense 支持的 Bug 修复 [（Microsoft Connect 项 #2453461）](https://connect.microsoft.com/SQLServer/feedback/details/2453461/sql-server-2012-issue-with-try-cast)。
3. SSMS 编辑器窗口中，允许拖放打开 Sql 文件的 Bug 修复 [（Microsoft Connect 项 #2690658）](https://connect.microsoft.com/SQLServer/feedback/details/2690658/cannot-drag-sql-files-into-management-studios)。
4. Analysis Services 中用于对多维 Analysis Services 模型正确显示数据馈送提供程序的 Bug 修复。
5. SSMS 中用于防止在尝试编辑 SSMS 表设计器中的联接链接时出现故障的 Bug 修复 [（Microsoft Connect 项 #2721052）](https://connect.microsoft.com/SQLServer/feedback/details/2721052/ssms-view-design-mode-right-click-on-join-crashes-ssms)。  

[可在 SSMS 更改日志中获取详细信息及更多 Bug 修复程序。](../ssms/sql-server-management-studio-changelog-ssms.md)

---
## <a name="downloadssdtmediadownloadpng-sql-server-management-studio-june-2016-releasehttpgomicrosoftcomfwlinklinkid799832"></a>![下载](../ssdt/media/download.png) [2016 年 6 月发行的 SQL Server Management Studio 版本](http://go.microsoft.com/fwlink/?LinkID=799832)

2016 年 6 月 1 日 | 版本号：13.0.15000.23

**功能**  
简化的新 SSMS 安装程序。 独立的 SSMS 版本。 自动检查更新。 新的“快速查找”对话框。 基于 Visual Studio 2015 Shell 等构建的 SSMS。   
[可在 SSMS 更改日志中获取详细信息。](../ssms/sql-server-management-studio-changelog-ssms.md)

**已知问题** 
1. **“始终加密”向导中的 PowerShell 脚本生成功能目前已禁用。**
此问题的修复程序将在后续的 SSMS 月度更新中提供。
2. **连接到 Azure SQL Database 时，将对表和列禁用对象资源管理器中的“加密列”上下文菜单项。** 此问题的修复程序将在后续的 SSMS 月度更新中提供。 作为一种解决方法，在对象资源管理器中右键单击你的数据库，选择“任务”，然后选择“加密列”以加密 Azure SQL Database 列和表。
3. **SSMS 只能连接到 SQL Server 2016 Integrated Services (SSIS 2016) 实例。** SQL Server Integration Services 存在已知的兼容性限制，会阻止与早期版本的连接。
作为此问题的一种解决方法，你可以使用匹配你的 SSIS 实例的 SSMS 版本连接到 SQL Server Integration Service 实例。
4. **SSMS 不会保存 SQL Server 2008 R2 和较早版本的 SQL Server 的维护计划。** 我们正在努力修复此问题。 与此同时，你可以使用 SSMS 2014 以下的版本来保存维护计划。
5. **如果客户端计算机上未安装 SQL Server，则SQL Server 配置管理器将无法启动。** 如果你未在自己的客户端计算机上安装 SQL Server，并启动了 SQL Server 配置管理器，你将收到“无法连接到 WMI 提供程序”错误。 解决方法如下：
    * 以管理员身份打开命令提示符。
    * 使用下列命令运行 Mofcomp 工具：  
      mofcomp "%programfiles(x86)%\Microsoft SQL Server\130\Shared\sqlmgmproviderxpsp2up.mof"
    * 在运行 Mofcomp 工具后，运行下列命令来重启 WMI 服务以使更改生效：  
       net stop "Windows Management Instrumentation"  
       net start "Windows Management Instrumentation"

**修复程序**  
1. SSMS 中的“快速查找”对话框，可以更好地集成到当前文档中并支持通过正则表达式进行搜索（[Microsoft Connect 项目 #2735513](https://connect.microsoft.com/SQLServer/feedback/details/2735513/quick-find-replace-in-ssms-2016-rc3/)）。
2. SSMS 上下文相关 F1 帮助中的 Bug 修复，可以正确显示帮助文档和文章。
3. 查询数据存储“回归查询”视图中导致 SSMS 在滚动时出现故障的 Bug 修复。
4. Excel Analysis Services OLEDB 连接器中的 Bug 修复，支持从 Excel 2016 到 SQL Server Analysis Services 的连接。
5. “SSMS 连接”对话框中的 Bug 修复，可以显示与多监视器系统的 SSMS 主窗口相同的监视器上的“连接”对话框（[Microsoft Connect 项目 #724909）](https://connect.microsoft.com/SQLServer/feedback/details/724909/connection-dialog-appears-off-screen/)。
6. “始终加密”体验的 Bug 修复。 修复了“始终加密”菜单项未正确针对延伸数据库启用的 Bug。 还修复了“始终加密”向导中未正确使用 SafeNet (Luna SA) HSM 提供程序的 Bug。

---
## <a name="downloadssdtmediadownloadpng-sql-server-management-studio-2014-sp1httpdownloadmicrosoftcomdownload156156992e6-f7c7-4e55-833d-249bd2348138enux86sqlmanagementstudiox86enuexe"></a>![下载](../ssdt/media/download.png) [SQL Server Management Studio 2014 SP1](http://download.microsoft.com/download/1/5/6/156992E6-F7C7-4E55-833D-249BD2348138/ENU/x86/SQLManagementStudio_x86_ENU.exe)

2015 年 5 月 14 日 | 版本号：12.0.4100.1

**功能**  
通过管理门户菜单中的新打开项、表设计器集成等改进了 Azure SQL Database 支持。   
[可在发行说明中获取详细信息](https://support.microsoft.com/en-us/kb/3058865)。

**已知问题**  
N/A

**修复程序**
1. 如果维护计划名称和首个 SUB_PLAN 名称相同，“维护计划变动”任务期间 SSMS 会出现故障。
2. 无法调试在 SQL Server Management Studio (SSMS) 中调用 sp_executesql 的存储过程。 按 F11 后，你会收到“对象引用未设置为对象的实例”错误消息（[Microsoft Connect 项目 #736509](https://connect.microsoft.com/SQLServer/feedback/details/736509/sql-server-2012-rtm-management-studio-cannot-debug-sp-executesql)）。
3. SSMS 不会完全管理 SQL Server Express 中的全文（[Microsoft Connect 项目 #740181](https://connect.microsoft.com/SQLServer/feedback/details/740181/management-studio-does-not-fully-manage-full-text-in-sql-server-express)）。
4. SSMS 对编号的存储过程的处理不一致 [（Microsoft Connect 项目 #764197](https://connect.microsoft.com/SQLServer/feedback/details/764197/ssms-2012-inconsistently-handles-numbered-procedures)）。
5. SSMS 有时会在关闭时出现故障，并导致其自动重启（[Microsoft Connect 项目 #774317](https://connect.microsoft.com/SQLServer/feedback/details/774317/sql-server-management-studio-2012-2014-crashes-when-closing)）。
6. 在 SSMS 中编写列级权限时创建脚本复制语句（[Microsoft Connect 项目 #797967](https://connect.microsoft.com/SQLServer/feedback/details/797967/ssms-create-script-duplicates-the-statements-for-grant-or-deny-column-permissions)）。
7. 尝试刷新任务栏上的 SSMS 窗口图标时 SSMS 可能会出现故障（[Microsoft Connect 项目 #799430](https://connect.microsoft.com/SQLServer/feedback/details/799430/ssms-2012-sp-1-cu-5-installed-crash-when-enforce-refresh-on-connect)）。

---
## <a name="downloadssdtmediadownloadpng-sql-server-management-studio-2012-sp3httpdownloadmicrosoftcomdownloadf67f673709c-d371-4a64-8bf9-c1dd73f60990enux86sqlmanagementstudiox86enuexe"></a>![下载](../ssdt/media/download.png) [SQL Server Management Studio 2012 SP3](http://download.microsoft.com/download/F/6/7/F673709C-D371-4A64-8BF9-C1DD73F60990/ENU/x86/SQLManagementStudio_x86_ENU.exe)  
  
2015 年 11 月 21 日 | 版本号：11.0.6020.0

**功能**  
功能全面的 SSMS 速成版。 代码段。 列存储索引等。  
[可在发行说明中获取详细信息。](https://support.microsoft.com/en-us/kb/3072779)
 
**已知问题**  
N/A

**修复程序**
1. 使用“导入和导出”向导导入数据时，缺失的列无法在错误消息中指示。
2. 还原 SSMS 中的差异备份时出现“由于 LSN 链接断开，无法创建还原计划”错误

---
## <a name="additional-downloads"></a>其他下载  
有关所有 SQL Server Management Studio 下载的列表，请搜索 [Microsoft 下载中心](https://www.microsoft.com/en-us/download/search.aspx?q=sql%20server%20management%20studio&p=0&r=10&t=&s=Relevancy~Descending)。  
  
有关最新版本的 SQL Server Management Studio 的信息，请参阅 [下载 SQL Server Management Studio &#40;SSMS&#41;](../ssms/download-sql-server-management-studio-ssms.md)。  

---  
## <a name="related-resources"></a>相关资源
[Microsoft SQL Server 的更新中心](https://technet.microsoft.com/sqlserver/ff803383.aspx)   
[SQL Server Management Studio 快速启动](http://msdn.microsoft.com/en-us/d2bade70-07cf-4d94-b5d2-88aecb538ed1)  
[SQL Server Management Studio 论坛](https://social.msdn.microsoft.com/forums/en-us/home?forum=sqltools)  

  

