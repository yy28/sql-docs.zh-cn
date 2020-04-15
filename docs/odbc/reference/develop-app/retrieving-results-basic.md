---
title: 检索结果（基本） |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3f7d01bf92fcee07940e449a2fb4bbac4f0fe6ac
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304328"
---
# <a name="retrieving-results-basic"></a>检索结果（基本）
*结果集*是数据源上的一组与特定条件匹配的行。 它是一个概念表，由查询生成，并且可用于表格形式的应用程序。 **选择**语句、目录函数和某些过程将创建结果集。 在下面的示例中，第一个 SQL 语句创建一个结果集，其中包含"订单"表中的所有行和所有列，第二个 SQL 语句为状态为 OPEN 的"订单"表中的行创建一个结果集：在"状态为打开"的"订单"表中，这些行包含 OrderID、SalesPerson 和状态列：  
  
```  
SELECT * FROM Orders  
SELECT OrderID, SalesPerson, Status FROM Orders WHERE Status = 'OPEN'  
```  
  
 结果集可以为空，这与没有结果集完全不同。 例如，以下 SQL 语句创建一个空结果集：  
  
```  
SELECT * FROM Orders WHERE 1 = 2  
```  
  
 空结果集与任何其他结果集没有什么不同，只是它没有行。 例如，应用程序可以检索结果集的元数据，可以尝试提取行，并且必须关闭结果集上的游标。  
  
 从数据源检索行并将其返回到应用程序的过程称为*提取*。 本节介绍该过程的基本部分。 有关更高级主题（如块和可滚动光标）的信息，请参阅[块光标](../../../odbc/reference/develop-app/block-cursors.md)和[可滚动游标](../../../odbc/reference/develop-app/scrollable-cursors.md)。 有关更新、删除和插入行的信息，请参阅[更新数据概述](../../../odbc/reference/develop-app/updating-data-overview.md)。  
  
 本部分包含以下主题。  
  
-   [是否创建了一个结果集？](../../../odbc/reference/develop-app/was-a-result-set-created.md)  
  
-   [结果集元数据](../../../odbc/reference/develop-app/result-set-metadata.md)  
  
-   [绑定列](../../../odbc/reference/develop-app/binding-columns.md)  
  
-   [提取数据](../../../odbc/reference/develop-app/fetching-data.md)  
  
-   [关闭游标](../../../odbc/reference/develop-app/closing-the-cursor.md)
