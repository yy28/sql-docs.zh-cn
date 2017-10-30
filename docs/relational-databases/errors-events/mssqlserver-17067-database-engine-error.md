---
title: MSSQLSERVER_17067 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 17067 (Database Engine error)
ms.assetid: 32c1f0e8-db70-4836-95b2-8833be9e0ad1
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ca8be81239735dc71265d6901faea9bbdef2b6bf
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver17067"></a>MSSQLSERVER_17067
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|17067|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|SQLASSERT_MESG|  
|消息正文|SQL Server 断言: 文件: \<%s>，行 = %d %s。 此错误可能与时间有关。 如果重新运行该语句后错误仍然存在，请使用 DBCC CHECKDB 来检查数据库的结构是否完整，或重新启动服务器以确保内存中的数据结构未破坏。|  
  
## <a name="explanation"></a>解释  
与时间有关的暂时性错误或内存中或磁盘上的数据损坏均可导致此错误。  
  
## <a name="user-action"></a>用户操作  
重新运行导致激发异常的语句。 如果错误是由与时间有关的事件导致的，则此错误可能不会重复发生。 如果问题仍然存在，请运行 DBCC CHECKDB 检查磁盘上的数据是否损坏。 重新启动服务器以确保内存中的数据结构未损坏。  
  
## <a name="see-also"></a>另请参阅  
[DBCC CHECKDB (Transact-SQL)](~/t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
  

