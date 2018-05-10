---
title: MSSQLSERVER_2596 | Microsoft Docs
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
- 2596 (Database Engine error)
ms.assetid: 49ab892f-8ba3-4ba1-b562-ddf205019802
caps.latest.revision: 18
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b71a0193c87814538f4891c3ced9a0553139e81c
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver2596"></a>MSSQLSERVER_2596
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|2596|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBCC_DATABASE_IN_READ_ONLY_MODE|  
|消息正文|未处理修复语句。 该数据库不能处于只读模式。|  
  
## <a name="explanation"></a>解释  
此消息指示数据库处于只读模式。 当数据库处于只读模式时不能进行修复。  
  
## <a name="user-action"></a>用户操作  
使用 ALTER DATABASE 设置要读写的数据库，然后重新运行 DBCC 命令。  
  
## <a name="see-also"></a>另请参阅  
[ALTER DATABASE (Transact-SQL)](~/t-sql/statements/alter-database-transact-sql-set-options.md)  
  
