---
title: SqlTriggerContext 对象 |Microsoft Docs
description: 在 SQL Server CLR 集成中，SqlTriggerContext 类为触发器（包括操作类型和在操作中修改的列）提供上下文信息。
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
ms.openlocfilehash: c6f11eda2ef791eb8c987af8d82149507770d47a
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2020
ms.locfileid: "91809153"
---
# <a name="sqltriggercontext-object"></a>SqlTriggerContext 对象
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  **SqlTriggerContext**类提供有关触发器的上下文信息。 此上下文信息包括导致触发器被激发的操作的类型、在更新操作中修改的列，以及在数据定义语言 (DDL) 触发器（用于描述触发操作的 XML **EventData** 结构）的情况下。 有关如何使用 **SqlTriggerContext** 类的详细信息和示例，请参阅 [CLR 触发器](/dotnet/framework/data/adonet/sql/clr-triggers)。  
  
 有关详细信息，请参阅 .NET Framework SDK 文档中的 **SqlTriggerContext** 类参考文档。  
  
## <a name="see-also"></a>另请参阅  
 [CLR 触发器](/dotnet/framework/data/adonet/sql/clr-triggers)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)  
  
