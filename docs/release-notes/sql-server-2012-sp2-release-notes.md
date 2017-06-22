---
title: "SQL Server 2012 SP2 发行说明 | Microsoft Docs"
ms.prod: sql-server-2012
ms.technology: server-general
ms.custom: 
ms.date: 01/31/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 67cb8b3e-3d82-47f4-840d-0f12a3bff565
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 5e132652cc6464502785647f8a79dec5e25094c4
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="sql-server-2012-sp2-release-notes"></a>SQL Server 2012 SP2 Release Notes
这些发行说明介绍了在安装 SQL Server 2012 Service Pack 2 或者解决其相关问题之前需要了解的问题。 发行说明仅在线提供，不提供相关安装介质。 发行说明会在发现问题时定期更新。 有关详细信息，请查阅 [SQL Server 2012 Service Pack 2 中修复的 Bug](http://support.microsoft.com/KB/2958429) 。  
  
## <a name="choose-the-correct-file-to-download-and-install"></a>正确选择要下载及安装的文件  
使用下表，基于您当前安装的版本识别要下载的文件的位置和名称。 下载页包含系统要求和基本安装说明。  
  
||||  
|-|-|-|  
|**当前安装的版本是...**|**而您需要...**|**请下载和安装...**|  
|32 位安装：|||  
|SQL Server 2012 的任何版本的 32 位版|升级到 SQL Server 2012 SP2 的 32 位版|**SQLServer2012SP2-KB2958429-**<arch>**-**<lang id>**.exe** ，来自 [SQL Server 2012 SP2 下载页](http://go.microsoft.com/fwlink/?LinkID=401006)|  
|SQL Server 2012 RTM Express 的 32 位版|升级到 SQL Server 2012 Express SP2 的 32 位版|**SQLEXPR_**<arch>**_**<lang>**.msi** ，来自 [SQL Server 2012 SP2 Express 下载页](http://go.microsoft.com/fwlink/?LinkID=401007)|  
|仅 SQL Server 2012 的客户端和可管理性工具（包括 SQL Server 2012 Management Studio）的 32 位版|将客户端和可管理性工具升级到 SQL Server 2012 SP2 的 32 位版|**SQLEXPRWT_**<arch>**_**<lang>**.msi** ，来自 [SQL Server 2012 SP2 Express 下载页](http://go.microsoft.com/fwlink/?LinkID=401007)|  
|SQL Server 2012 Management Studio Express 的 32 位版|升级到 SQL Server 2012 SP2 Management Studio Express 的 32 位版|**SQLManagementStudio_**<arch>**_**<lang>**.msi** ，来自 [SQL Server 2012 SP2 Express 下载页](http://go.microsoft.com/fwlink/?LinkID=401007)|  
|SQL Server 2012 的任何版本的 32 位版以及客户端和管理工具（包括 SQL Server 2012 RTM Management Studio）的 32 位版|将所有产品都升级到 SQL Server 2012 SP2 的 32 位版|**SQLEXPRADV_**<arch>**_**<lang>**.msi** ，来自 [SQL Server 2012 SP2 Express 下载页](http://go.microsoft.com/fwlink/?LinkID=401007)|  
|[Microsoft SQL Server 2012 RTM 功能包](http://www.microsoft.com/download/details.aspx?id=29065) (#microsoft-sql-server-2012-rtm-功能包) 或 [Microsoft SQL Server 2012 SP1 功能包](http://go.microsoft.com/fwlink/p/?LinkID=268266)(#microsoft-sql-server-2012-sp1-功能包) 中一种或多种工具的 32 位版|将工具升级到 Microsoft SQL Server 2012 SP2 功能包的 32 位版|Microsoft [SQL Server 2012 SP2 功能包下载页](http://go.microsoft.com/fwlink/?LinkID=401008)中的一种或多种工具|  
|64 位安装：|||  
|SQL Server 2012 的任何版本的 64 位版|升级到 SQL Server 2012 SP2 的 64 位版|SQLServer2012SP2-KB2958429-<arch>-<langid>.exe，来自 [SQL Server 2012 SP2 下载页](http://go.microsoft.com/fwlink/?LinkID=401006)(#sql-server-2012-sp2-下载页)|  
|SQL Server 2012 RTM Express 的 64 位版|升级到 SQL Server 2012 SP2 的 64 位版|**SQLEXPR_**<arch>**_**<lang>**.msi** ，来自 [SQL Server 2012 SP2 Express 下载页](http://go.microsoft.com/fwlink/?LinkID=401007)|  
|仅 SQL Server 2012 的客户端和可管理性工具（包括 SQL Server 2012 R2 Management Studio）的 32 位版|将客户端和可管理性工具升级到 SQL Server 2012 SP2 的 64 位版|**SQLEXPRWT_**<arch>**_**<lang>**.msi** ，来自 [SQL Server 2012 SP2 Express 下载页](http://go.microsoft.com/fwlink/?LinkID=401007)|  
|SQL Server 2012 Management Studio Express 的 64 位版|升级到 SQL Server 2012 SP2 Management Studio Express 的 64 位版|**SQLManagementStudio_**<arch>**_**<lang>**.msi** ，来自 [SQL Server 2012 SP2 Express 下载页](http://go.microsoft.com/fwlink/?LinkID=401007)|  
|[Microsoft SQL Server 2012 RTM 功能包](http://www.microsoft.com/download/details.aspx?id=29065) (#microsoft-sql-server-2012-rtm-功能包) 或 [Microsoft SQL Server 2012 SP1 功能包](http://go.microsoft.com/fwlink/p/?LinkID=268266)(#microsoft-sql-server-2012-sp1-功能包) 中一种或多种工具的 64 位版|将工具升级到 Microsoft SQL Server 2012 SP2 功能包的 64 位版|Microsoft [SQL Server 2012 SP2 功能包下载页](http://go.microsoft.com/fwlink/?LinkID=401008)中的一种或多种工具|  
  

