---
title: MSSQLSERVER_2518 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 2518 (Database Engine error)
ms.assetid: 54a13abc-4c33-43f0-b55d-e2e74a1381c8
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ca6a654894304197357cbe244be60f9b9a58f789
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "68138505"
---
# <a name="mssqlserver_2518"></a>MSSQLSERVER_2518
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|2518|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBCC_NO_EXPRESSION_EVAL_CLR_DISABLED|  
|消息正文|对象 ID O_ID（对象 "O_NAME"）: 由于禁用了公共语言运行时 (CLR)，因此无法检查此对象的计算列和用户定义类型。|  
  
## <a name="explanation"></a>说明  
此信息性消息指示，查询处理器无法为 DBCC 提供内部对象，以允许对计算列和公共语言运行时 (CLR) 用户定义类型进行计算。 之所以出现此问题，是因为其中一个列涉及 CLR，但未启用 CLR。 内部对象涉及所有列。 因此，无法计算单个列将阻止创建内部对象。 这意味着在 DBCC 检查索引和基表之间的一致性时，将不检查计算列是否正确或使用它们。  
  
## <a name="user-action"></a>用户操作  
启用 CLR 并重新运行 DBCC 语句。  
  
## <a name="see-also"></a>另请参阅  
[启用 CLR 集成](~/relational-databases/clr-integration/clr-integration-enabling.md)  
  
