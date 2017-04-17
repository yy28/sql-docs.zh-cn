---
title: "SQL Server Management Studio - 发行说明 | Microsoft Docs"
ms.custom: 
ms.date: 01/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0b95337b-80bf-4624-8f5d-cdaf6181d3b8
caps.latest.revision: 51
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 51e336a22d0c1052c48b8e569330aef26f2af094
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-management-studio----release-notes"></a>SQL Server Management Studio - 发行说明
欢迎使用我们的 SQL Server Management Studio 公开发布版本！  此版本的 SQL Server Management Studio (SSMS) 是 SQL Server 版本外部的独立安装。 我们的目标是频繁更新其新功能、修复程序以及对 SQL Server 和 Azure SQL Database 中最新功能的支持。  
  
若要安装最新版本的 SQL Server Management Studio，请参阅 [下载 SQL Server Management Studio &#40;SSMS&#41;](../ssms/download-sql-server-management-studio-ssms.md)。  
  
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

## <a name="feedback"></a>反馈  
  
![needhelp_person_icon](../ssms/media/needhelp_person_icon.png) [SQL 客户端工具论坛](https://social.msdn.microsoft.com/Forums/en-US/home?forum=sqltools) |  [在 Microsoft Connect 中提出问题或建议](https://connect.microsoft.com/SQLServer/Feedback)。  
  
## <a name="see-also"></a>另请参阅  
[SQL Server Management Studio 教程](../ssms/use-sql-server-management-studio.md)  
[下载 SQL Server Management Studio &amp;#40;SSMS&amp;#41;](../ssms/download-sql-server-management-studio-ssms.md)  
[以前的 SQL Server Management Studio 版本](../ssms/previous-sql-server-management-studio-releases.md)  

  

