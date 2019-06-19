---
title: MSSQLSERVER_10003 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10003 (Database Engine error)
ms.assetid: 9e2cb199-f077-4d88-8117-1b7550afc696
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 674a068985b3de4c89f85c1878344ef665cc0511
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63048992"
---
# <a name="mssqlserver10003"></a>MSSQLSERVER_10003
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|10003|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|HR_E_OUTOFMEMORY|  
|消息正文|提供程序内存不足。|  
  
## <a name="explanation"></a>解释  
系统内存不足导致 OLE DB 访问接口内存不足。  
  
## <a name="user-action"></a>用户操作  
重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例。 如果无效，请重新启动计算机。 如果问题仍然存在，请使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 收集 OLE DB 跟踪事件，并向 OLE DB 提供程序的产品支持人员提供此数据。  
  
## <a name="see-also"></a>另请参阅  
[SQL Server Profiler 模板和权限](~/tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)  
[SQL Server Native Client (OLE DB)](~/relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
