---
title: MSSQLSERVER_17065 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 17065 (Database Engine error)
ms.assetid: 63c2ba5a-be34-461e-bee1-03c25b396cd2
caps.latest.revision: 16
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bac1e9055e83ad27a99fa6fb83b3c0ac9e9a5d46
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver17065"></a>MSSQLSERVER_17065
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|17065|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|SQLASSERT_BOTH|  
|消息正文|SQL Server 断言: 文件: \<%s>，行 = %d 失败的断言 = '%s' %s。 此错误可能与时间有关。 如果重新运行该语句后错误仍然存在，请使用 DBCC CHECKDB 来检查数据库的结构是否完整，或重新启动服务器以确保内存中的数据结构未破坏。|  
  
## <a name="explanation"></a>解释  
与时间有关的暂时性错误或内存中或磁盘上的数据损坏均可导致此错误。  
  
## <a name="user-action"></a>用户操作  
重新运行导致激发异常的语句。 如果错误是由与时间有关的事件导致的，则此错误可能不会重复发生。 如果问题仍然存在，请运行 DBCC CHECKDB 检查磁盘上的数据是否损坏。 重新启动服务器以确保内存中的数据结构未损坏。  
  
## <a name="see-also"></a>另请参阅  
[DBCC CHECKDB (Transact-SQL)](~/t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
  
