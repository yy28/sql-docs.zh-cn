---
title: MSSQLSERVER_10001 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 10001 (Database Engine error)
ms.assetid: f8fd2d8d-a4af-4b6a-ba51-9123b7e4c9bf
caps.latest.revision: "16"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c783a94811086b7bb03d392220781f3757947d68
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver10001"></a>MSSQLSERVER_10001
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|10001|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|HR_E_UNEXPECTED|  
|消息正文|提供程序报告了意外的灾难性错误。|  
  
## <a name="explanation"></a>解释  
分布式查询处理在调用 OLE DB 访问接口期间遇到一个一般性错误。  
  
## <a name="user-action"></a>用户操作  
使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 收集 OLE DB 跟踪事件并向 OLE DB 提供程序的产品支持人员提供此数据。  
  
## <a name="see-also"></a>另请参阅  
[SQL Server Profiler 模板和权限](~/tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)  
[SQL Server Native Client (OLE DB)](~/relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
