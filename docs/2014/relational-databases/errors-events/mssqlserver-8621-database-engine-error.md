---
title: MSSQLSERVER_8621 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 8621 (Database Engine error)
ms.assetid: 67f59865-becd-4999-8bb0-90aedd7effbf
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e054232776435a5d7825427393e6fbfa0bf232d6
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85053557"
---
# <a name="mssqlserver_8621"></a>MSSQLSERVER_8621
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|8621|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|OPTIMIZER_STACK_OVERFLOW_ERR|  
|消息正文|查询处理器在优化查询时堆栈空间不足。 请简化查询。|  
  
## <a name="explanation"></a>说明  
 出错的最可能原因是扩展查询的大小。 在每个视图的定义、计算列、[!INCLUDE[tsql](../../includes/tsql-md.md)] 函数和它引用的公用表表达式以及级联操作（如更新辅助索引、视图和触发器）方面，扩展查询将替换原始查询。  
  
 很可能查询在某个维度中很大；例如，视图定义所引用的表数，或者很大的标量表达式。  
  
## <a name="user-action"></a>用户操作  
 通过沿最大维度将该查询分解为多个查询，对其进行简化。 首先删除实际上不需要的任何查询元素，然后尝试添加临时表并将该查询拆分为两个查询。  仅将查询的一部分移动到子查询、函数或公用表表达式是不够的，因为 [!INCLUDE[tsql](../../includes/tsql-md.md)] 编译器会将它们重新组合在一起。  
  
  
