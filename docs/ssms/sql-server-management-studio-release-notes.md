---
title: "SQL Server Management Studio - 发行说明 | Microsoft Docs"
ms.custom: 
ms.date: 06/22/2017
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
ms.translationtype: Human Translation
ms.sourcegitcommit: fe6de2b16b9792a5399b1c014af72a2a5ee52377
ms.openlocfilehash: f593303a681e2f52161777fc48f0fb1b479d20d9
ms.contentlocale: zh-cn
ms.lasthandoff: 06/23/2017

---
<a id="sql-server-management-studio----release-notes" class="xliff"></a>

# SQL Server Management Studio - 发行说明
欢迎使用我们的 SQL Server Management Studio 公开发布版本！  此版本的 SQL Server Management Studio (SSMS) 是 SQL Server 版本外部的独立安装。 我们的目标是频繁更新其新功能、修复程序以及对 SQL Server 和 Azure SQL Database 中最新功能的支持。  
  
若要安装最新版本的 SQL Server Management Studio，请参阅 [下载 SQL Server Management Studio &#40;SSMS&#41;](../ssms/download-sql-server-management-studio-ssms.md)。  
  
以下是此 SQL Server Management Studio 版本的问题和限制：  

1. **还原数据库向导将生成为目标数据库文件的位置不正确的路径模式**
    SSMS 连接到 Linux 服务器时，这是一个已知的问题。 虽然路径看起来不正确/奇数，则它在服务器端正确地处理，即未出现功能问题。

2. **文件浏览器问题**
    - 在使用基于 Windows 的 SQL Server 自 2017 年 1 CTP 2.0 实例，文件浏览器中 SSMS UI 可能无法打开如果服务器具有空的软盘驱动器或固定的磁盘安装的 Bitlocker 的保护。 
    - 文件浏览器的 UI 不再支持的 SQL Server 自 2017 年在 CTP 2.0 之前的版本。
    


3. **仅单个 Azure Active Directory 帐户可以使用 Active Directory 通用身份验证为 SSMS 实例登录。**  
    此限制仅限于 Active Directory 通用身份验证 - 你可以使用 Active Directory 密码身份验证、Active Directory 集成身份验证或 SQL Server 身份验证登录不同的服务器。
    
    作为一种解决方法，你可以使用 SSMS 的其他实例以另一个 Azure Active Directory 帐户身份登录。 
    
4. **SSMS 中的数据层应用程序框架 (DacFx) 命令和架构设计器不支持 Active Directory 通用身份验证。**  
    使用 SSMS 中的 DacFx 架构设计器的命令（例如，导入和导出）目前不支持 Active Directory 通用身份验证。
    
    作为一种解决方法，你可以使用 SSMS 中提供的其他形式的身份验证 - Active Directory 密码身份验证、Active Directory 集成身份验证或 SQL Server 身份验证。

5. **SSMS 只能连接到 SQL Server 2016 Integrated Services (SSIS 2016) 实例。**  
    SQL Server Integration Services 存在已知的兼容性限制，会阻止与早期版本的连接。
    
    作为此问题的一种解决方法，你可以使用 [匹配你的 SSIS 实例的 SSMS 版本](../ssms/previous-sql-server-management-studio-releases.md)连接到 SQL Server Integration Service 实例 
  
5. **SSMS 不会保存 SQL Server 2008 R2 和较早版本的 SQL Server 的维护计划。**  
    我们希望此已知限制在以后得以解决。 与此同时，你可以使用 [SSMS 2014 版本](../ssms/previous-sql-server-management-studio-releases.md) 来保存维护计划。  
    
5. **非英语版 SSMS 安装可能需要安装其他安全包。**  
如果安装在以下系统中，则非英语本地化版本的 SSMS [需要 KB 2862966 安全更新程序包](https://support.microsoft.com/en-us/kb/2862966) ：Windows 8、Windows 7、Windows Server 2012 和 Windows Server 2008 R2。

5. **无法通过单击“帮助”或按 F1 打开帮助**  
单击“帮助”或按 F1 可能会在一些环境中看到以下错误消息：“必须有新应用，才能打开 ms-xhelp”。 此错误为已知问题，将在即将发布的版本中得到修复。
  
<a id="feedback" class="xliff"></a>

## 反馈  
  
![needhelp_person_icon](../ssms/media/needhelp_person_icon.png) [SQL 客户端工具论坛](https://social.msdn.microsoft.com/Forums/en-US/home?forum=sqltools) |  [在 Microsoft Connect 中提出问题或建议](https://connect.microsoft.com/SQLServer/Feedback)。  
  
<a id="see-also" class="xliff"></a>

## 另请参阅  
[SQL Server Management Studio 教程](../ssms/use-sql-server-management-studio.md)  
[下载 SQL Server Management Studio &amp;#40;SSMS&amp;#41;](../ssms/download-sql-server-management-studio-ssms.md)  
[以前的 SQL Server Management Studio 版本](../ssms/previous-sql-server-management-studio-releases.md)  

  

