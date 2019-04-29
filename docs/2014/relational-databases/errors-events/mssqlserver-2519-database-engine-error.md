---
title: MSSQLSERVER_2519 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 2519 (Database Engine error)
ms.assetid: 8dc6ad98-5db8-4c88-8dea-6d455e63b839
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ec6663028f2c0e133996053a31acfc0e04b49738
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62914676"
---
# <a name="mssqlserver2519"></a>MSSQLSERVER_2519
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|2519|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|DBCC_NO_EXPRESSION_EVALUATOR|  
|消息正文|由于无法初始化内部的表达式计算器，从而无法检查对象 ID O_ID（对象 "O_NAME"）的计算列和用户定义类型。|  
  
## <a name="explanation"></a>解释  
 此信息性消息指示，查询处理器无法为 DBCC 提供内部对象，以允许对计算列和公共语言运行时 (CLR) 用户定义类型进行计算。 这意味着在 DBCC 检查索引和基表之间的一致性时，将不检查计算列和 CLR 用户定义类型是否正确或使用它们。  
  
## <a name="user-action"></a>用户操作  
 None  
  
## <a name="see-also"></a>请参阅  
 [MSSQLSERVER_2518](mssqlserver-2518-database-engine-error.md)  
  
  
