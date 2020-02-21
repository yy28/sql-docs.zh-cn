---
title: 选择与值不匹配的行
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- search conditions [SQL Server], rows not matching value
- row not matching value [SQL Server]
- NOT operator [Visual Database Tools]
- search criteria [SQL Server], rows not matching value
ms.assetid: 19898578-7b2f-401c-bb8f-9f2a017efdf7
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.openlocfilehash: ba594307277060abd6ddedb9dd7fda7c1a8bebee
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "75255093"
---
# <a name="select-rows-that-do-not-match-a-value-visual-database-tools"></a>选择与值不匹配的行 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
若要查找与某值不匹配的行，可以使用 NOT 运算符。  
  
### <a name="to-find-rows-that-do-not-match-a-value"></a>查找与某值不匹配的行  
  
1.  如果尚未指定搜索条件，请将要在搜索条件内使用的列或表达式添加到 [“条件”窗格](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)中。  
  
2.  找到包含要搜索的数据列或表达式的行，然后在“筛选器”网格列中，顺序输入 NOT 运算符和搜索值。  
  
例如，若要在 `products` 表中查找产品代码列中的值以“A”之外的其他字符开头的所有行，则可以输入如下搜索条件：  
  
```  
NOT LIKE 'A%'  
```  
  
## <a name="see-also"></a>另请参阅  
[针对输入搜索值的规则](../../ssms/visual-db-tools/rules-for-entering-search-values-visual-database-tools.md)  
[指定搜索条件](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  
