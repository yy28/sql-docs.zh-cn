---
title: "MSSQLSERVER - 数据库引擎错误 | Microsoft Docs"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 823 (Database Engine error)
ms.assetid: 0d9fce3c-3772-46ce-a7a3-4f4988dc6cae
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 453ab7e66fe46fb00660d2f5220907703bc096a6
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver---database-engine-error"></a>MSSQLSERVER - 数据库引擎错误
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|823|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|B_HARDERR|  
|消息正文|在文件 '%ls' 中、偏移量为 %#016I64x 的位置执行 %S_MSG 期间，操作系统已经向 SQL Server 返回了错误 %ls。 SQL Server 错误日志和系统事件日志中的其他消息中可能有更详细的信息。 这是一个威胁数据库完整性的严重系统级错误条件，必须立即纠正。 请运行一次完整的数据库一致性检查 (DBCC CHECKDB)。 此错误可能是由多种因素导致的；有关详细信息，请参阅 SQL Server 联机丛书。|  
  
## <a name="explanation"></a>解释  
Windows 读取或写入请求失败。 将 Windows 返回的错误代码和相应的文本插入到消息中。 对于读取操作，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已经重试读取请求四次。 通常是硬件错误导致此错误，但也可能是设备驱动程序导致的。 有关错误 823 的详细信息，请参阅 [http://support.microsoft.com/kb/828339](http://support.microsoft.com/kb/828339)。 有关 I/O 错误的详细信息，请参阅 [Microsoft SQL Server I/O 基础知识，第 2 章](http://go.microsoft.com/fwlink/?LinkId=69370)。  
  
## <a name="user-action"></a>用户操作  
查看系统事件日志中的其他信息。 与硬件制造商或 Microsoft 客户服务与支持部门联系，以确定原因和纠正操作。 在修复硬件错误后，还原所有数据库并运行 DBCC CHECKDB。  
  
