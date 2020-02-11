---
title: SqlTriggerContext 对象 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- SqlTriggerContext object
- triggers [CLR integration]
- context [CLR integration]
ms.assetid: 472a2d0b-64ae-4877-8f11-a5620aa698b7
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: df384324ba16aac03a4c889cf4f3959c23374510
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62874694"
---
# <a name="sqltriggercontext-object"></a>SqlTriggerContext 对象
  
  `SqlTriggerContext` 类提供有关触发器的上下文信息。 该上下文信息包括导致触发器被激发的操作的类型，以及在 UPDATE 操作中进行了修改的列，如果是数据定义语言 (DDL) 触发器，则还包括描述触发操作的 XML `EventData` 结构。 有关如何使用`SqlTriggerContext`类的详细信息和示例，请参阅[CLR 触发器](../../database-engine/dev-guide/clr-triggers.md)。  
  
 有关详细信息，请参阅`Microsoft.SqlServer.Server.SqlTriggerContext` .NET Framework SDK 文档中的类参考文档。  
  
## <a name="see-also"></a>另请参阅  
 [CLR 触发器](../../database-engine/dev-guide/clr-triggers.md)   
 [EVENTDATA (Transact-SQL)](/sql/t-sql/functions/eventdata-transact-sql)  
  
  
