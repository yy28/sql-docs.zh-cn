---
title: SqlTriggerContext 对象 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SqlTriggerContext object
- triggers [CLR integration]
- context [CLR integration]
ms.assetid: 472a2d0b-64ae-4877-8f11-a5620aa698b7
caps.latest.revision: 18
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: dbdaefa1e3c5e1c5a53cd6179f4b96320434dbdf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015901"
---
# <a name="sqltriggercontext-object"></a>SqlTriggerContext 对象
  `SqlTriggerContext` 类提供有关触发器的上下文信息。 该上下文信息包括导致触发器被激发的操作的类型，以及在 UPDATE 操作中进行了修改的列，如果是数据定义语言 (DDL) 触发器，则还包括描述触发操作的 XML `EventData` 结构。 有关详细信息和如何使用的示例`SqlTriggerContext`类，请参阅[CLR 触发器](../../database-engine/dev-guide/clr-triggers.md)。  
  
 有关详细信息，请参阅`Microsoft.SqlServer.Server.SqlTriggerContext`类参考文档中的.NET Framework SDK 文档。  
  
## <a name="see-also"></a>请参阅  
 [CLR 触发器](../../database-engine/dev-guide/clr-triggers.md)   
 [EVENTDATA (Transact-SQL)](/sql/t-sql/functions/eventdata-transact-sql)  
  
  
