---
title: MSSQLSERVER_125 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- "125"
helpviewer_keywords:
- 125 (Database Engine error)
ms.assetid: 0f58338d-2ea0-48b8-8a20-c438b0940433
caps.latest.revision: 10
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: c2739d0dace0b1cd1180611d406abb9bc88f56a4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36018886"
---
# <a name="mssqlserver125"></a>MSSQLSERVER_125
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|125|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称||  
|消息正文|Case 表达式只能嵌套到 %d 层。|  
  
## <a name="explanation"></a>解释  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 仅允许在 CASE 表达式中嵌套 10 个级别。  
  
## <a name="user-action"></a>用户操作  
 将 CASE 语句的级别减少到 10 级或更低的级数。  
  
## <a name="see-also"></a>请参阅  
 [CASE (Transact-SQL)](/sql/t-sql/language-elements/case-transact-sql)  
  
  
