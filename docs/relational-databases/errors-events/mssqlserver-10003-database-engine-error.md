---
description: MSSQLSERVER_10003
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
ms.openlocfilehash: d25d4a203c5871c4d9542c03e3872dd1206bb543
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88339633"
---
# <a name="mssqlserver_10003"></a>MSSQLSERVER_10003
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>详细信息  
  
| Attribute | 值 |  
| :-------- | :---- |  
|产品名称|SQL Server|  
|事件 ID|10003|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|HR_E_OUTOFMEMORY|  
|消息正文|提供程序内存不足。|  
  
## <a name="explanation"></a>说明  
系统内存不足导致 OLE DB 访问接口内存不足。  
  
## <a name="user-action"></a>用户操作  
重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例。 如果无效，请重新启动计算机。 如果问题仍然存在，请使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 收集 OLE DB 跟踪事件，并向 OLE DB 提供程序的产品支持人员提供此数据。  
  
## <a name="see-also"></a>另请参阅  
[SQL Server Profiler 模板和权限](~/tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)  
[SQL Server Native Client (OLE DB)](~/relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
