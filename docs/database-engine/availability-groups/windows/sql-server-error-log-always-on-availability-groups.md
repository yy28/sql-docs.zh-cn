---
title: SQL Server 错误日志（Always On 可用性组）(SQL Server) | Microsoft Docs
ms.custom: ag-guide
ms.date: 06/13/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 39d0c98d-75af-4dd1-b908-30d31af56f2a
author: rothja
ms.author: jroth
ms.openlocfilehash: 3152d98e44f723ed15f508e76d9828eb6dde82c6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68013975"
---
# <a name="sql-server-error-log-always-on-availability-groups"></a>SQL Server 错误日志（Always On 可用性组）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  SQL Server 错误日志报告影响 Always On 可用性组的事件，如：  
  
-   与 Windows Server 故障转移群集 (WSFC) 群集的通信    
-   可用性副本的状态转换    
-   可用性数据库的状态转换    
-   主要副本和次要副本之间的可用性数据库的连接状态    
-   可用性组终结点的状态    
-   可用性组侦听程序的状态    
-   SQL Server 资源 DLL（在 WSFC 群集中运行）和 SQL Server 实例之间的租用状态（有关详细信息，请参阅 [How It Works:How It Works: SQL Server Always On lease timeout](https://blogs.msdn.com/b/psssql/archive/2012/09/07/how-it-works-sql-server-alwayson-lease-timeout.aspx)（工作原理：SQL Server Always On 租用超时））    
-   可用性组中的错误事件  

出现以下症状时应查看 SQL Server 错误日志：  

-   无法访问可用性数据库    
-   意外的可用性组故障转移    
-   可用性组意外处于“正在解决”状态    
-   可用性组处于不确定状态  
  
有关详细信息，请参阅[查看 SQL Server 错误日志 (SQL Server Management Studio)](~/relational-databases/performance/view-the-sql-server-error-log-sql-server-management-studio.md)。  
  
  
