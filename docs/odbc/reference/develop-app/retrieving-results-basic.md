---
title: 检索结果（基本） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], about result sets
- data sources [ODBC], result sets
- empty result sets [ODBC]
ms.assetid: 052870e3-3f3f-4f07-91da-b649348225f4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7abe4dd2f0bfb0b5302022d8e50cddc7df84f192
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68020467"
---
# <a name="retrieving-results-basic"></a>检索结果（基本）
*结果集*是与特定条件匹配的数据源中的一组行。 它是一个由查询生成的概念表，可用于表格格式的应用程序。 **SELECT**语句、目录函数和某些过程会创建结果集。 在下面的示例中，第一个 SQL 语句创建一个结果集，其中包含 Orders 表中的所有行和所有列，第二个 SQL 语句为 Orders 表中的行创建包含 "订单 Id"、"销售人员" 和 "状态" 列的结果集状态处于打开状态：  
  
```  
SELECT * FROM Orders  
SELECT OrderID, SalesPerson, Status FROM Orders WHERE Status = 'OPEN'  
```  
  
 结果集可以是空的，这与根本没有结果集不同。 例如，下面的 SQL 语句创建了一个空的结果集：  
  
```  
SELECT * FROM Orders WHERE 1 = 2  
```  
  
 空结果集与其他任何结果集没有任何区别，只不过它没有行。 例如，应用程序可以检索结果集的元数据，可以尝试提取行，并且必须在结果集上关闭游标。  
  
 从数据源检索行并将其返回到应用程序的过程称为*提取*。 本部分介绍了该过程的基本部分。 有关更高级的主题（如 block 和可滚动游标）的信息，请参阅[块游标](../../../odbc/reference/develop-app/block-cursors.md)和可[滚动游标](../../../odbc/reference/develop-app/scrollable-cursors.md)。 有关更新、删除和插入行的信息，请参阅[更新数据概述](../../../odbc/reference/develop-app/updating-data-overview.md)。  
  
 本部分包含下列主题。  
  
-   [是否创建了一个结果集？](../../../odbc/reference/develop-app/was-a-result-set-created.md)  
  
-   [结果集元数据](../../../odbc/reference/develop-app/result-set-metadata.md)  
  
-   [绑定列](../../../odbc/reference/develop-app/binding-columns.md)  
  
-   [提取数据](../../../odbc/reference/develop-app/fetching-data.md)  
  
-   [关闭游标](../../../odbc/reference/develop-app/closing-the-cursor.md)
