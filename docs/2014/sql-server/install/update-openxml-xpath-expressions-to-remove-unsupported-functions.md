---
title: 更新 OPENXML XPath 表达式以删除不支持的函数 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- OPENXML queries
ms.assetid: b459abaf-8787-4b65-9231-ae30e5469fd0
caps.latest.revision: 17
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 768124887a7d75797229919d7d7399df9ce4b130
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36123758"
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
 [SQL Server 2014 升级顾问&#91;新&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
