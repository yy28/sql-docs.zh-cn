---
title: SqlTriggerContext 对象 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: clr
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SqlTriggerContext object
- triggers [CLR integration]
- context [CLR integration]
ms.assetid: 472a2d0b-64ae-4877-8f11-a5620aa698b7
caps.latest.revision: 18
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: ff176908a3ef66f9c1d14d1c5a695932075e8735
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37353269"
---
# <a name="sqltriggercontext-object"></a>SqlTriggerContext 对象
  `SqlTriggerContext` 类提供有关触发器的上下文信息。 该上下文信息包括导致触发器被激发的操作的类型，以及在 UPDATE 操作中进行了修改的列，如果是数据定义语言 (DDL) 触发器，则还包括描述触发操作的 XML `EventData` 结构。 有关详细信息和示例的用法`SqlTriggerContext`类，请参阅[CLR 触发器](../../database-engine/dev-guide/clr-triggers.md)。  
  
 有关详细信息，请参阅`Microsoft.SqlServer.Server.SqlTriggerContext`类在.NET Framework SDK 文档中的参考文档。  
  
## <a name="see-also"></a>请参阅  
 [CLR 触发器](../../database-engine/dev-guide/clr-triggers.md)   
 [EVENTDATA (Transact-SQL)](/sql/t-sql/functions/eventdata-transact-sql)  
  
  
