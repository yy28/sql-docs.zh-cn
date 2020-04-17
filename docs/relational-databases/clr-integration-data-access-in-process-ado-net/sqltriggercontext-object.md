---
title: SqlTrigger上下文对象 |微软文档
description: 在 SQL Server CLR 集成中，SqlTriggerContext 类为触发器提供上下文信息，包括操作类型和在操作中修改的列。
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
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
ms.openlocfilehash: 55e0ac850071615d9be7fb47442ed674eefab00a
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487456"
---
# <a name="sqltriggercontext-object"></a>SqlTriggerContext 对象
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **SqlTriggerContext**类提供有关触发器的上下文信息。 此上下文信息包括导致触发器触发的操作类型、更新操作中修改的列，以及数据定义语言 （DDL） 触发器（描述触发操作的 XML EventData 结构）中的 XML **EventData**结构。 有关如何使用**SqlTriggerContext**类的详细信息和示例，请参阅[CLR 触发器](https://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c)。  
  
 有关详细信息，请参阅 .NET 框架 SDK 文档中的**Microsoft.SqlServer.Server.SqlTriggerContext**类引用文档。  
  
## <a name="see-also"></a>另请参阅  
 [CLR 触发器](https://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
