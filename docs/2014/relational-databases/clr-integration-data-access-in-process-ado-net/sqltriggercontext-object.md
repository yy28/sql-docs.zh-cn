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
ms.openlocfilehash: f7eae3d290a70bedee0ed9badf9e6d0503caa2bc
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84955007"
---
# <a name="sqltriggercontext-object"></a>SqlTriggerContext 对象
  `SqlTriggerContext` 类提供有关触发器的上下文信息。 该上下文信息包括导致触发器被激发的操作的类型，以及在 UPDATE 操作中进行了修改的列，如果是数据定义语言 (DDL) 触发器，则还包括描述触发操作的 XML `EventData` 结构。 有关如何使用类的详细信息和示例 `SqlTriggerContext` ，请参阅[CLR 触发器](../../database-engine/dev-guide/clr-triggers.md)。  
  
 有关详细信息，请参阅 `Microsoft.SqlServer.Server.SqlTriggerContext` .NET FRAMEWORK SDK 文档中的类参考文档。  
  
## <a name="see-also"></a>另请参阅  
 [CLR 触发器](../../database-engine/dev-guide/clr-triggers.md)   
 [EVENTDATA (Transact-SQL)](/sql/t-sql/functions/eventdata-transact-sql)  
  
  
