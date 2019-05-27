---
title: 更新 OPENXML XPath 表达式以删除不受支持的函数 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- OPENXML queries
ms.assetid: b459abaf-8787-4b65-9231-ae30e5469fd0
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ec0edb2e72143fd41709355a3e9cc338544289a6
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66091686"
---
# <a name="update-openxml-xpath-expressions-to-remove-unsupported-functions"></a>更新 OPENXML XPath 表达式以删除不支持的函数
  升级顾问检测到使用了 XPath 功能。 升级后，对 OPENXML 功能的 XPath 功能所做的更改可能产生影响。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 MSXML 3.0 现为基础引擎，用于处理 OPENXML 查询中使用的 XPath 表达式。 MSXML 3.0 的 XPath 1.0 引擎更为严格，且删除了对以下函数的支持：  
  
-   format-number()  
  
-   formatNumber()  
  
-   current()  
  
-   element-available()  
  
-   function-available()  
  
-   system-property()  
  
## <a name="corrective-action"></a>纠正措施  
 对于 format-number() 和 formatNumber()，可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)]。 对于前面列出的其他不支持的函数，没有直接的解决方法。  
  
## <a name="see-also"></a>请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问&#91;新&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
