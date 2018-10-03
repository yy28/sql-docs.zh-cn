---
title: 检索结果 （基本） |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 8eb98d7c17663894e1bacdc27e431d6a54f45d3b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47772205"
---
# <a name="retrieving-results-basic"></a>检索结果（基本）
一个*结果集*是一组与某些条件匹配的数据源上的行。 它是一个概念性的表的查询的结果，即以表格形式的应用程序可以。 **选择**语句、 目录函数和某些过程创建结果集。 在以下示例中，第一条 SQL 语句创建包含所有行和 Orders 表中的所有列的结果集和第二个 SQL 语句将创建包含订单表中的行的 OrderID、 销售人员和状态列的结果集在其中状态是已打开：  
  
```  
SELECT * FROM Orders  
SELECT OrderID, SalesPerson, Status FROM Orders WHERE Status = 'OPEN'  
```  
  
 结果集可以为空，即没有结果集中完全不同。 例如，以下 SQL 语句创建一个空结果集：  
  
```  
SELECT * FROM Orders WHERE 1 = 2  
```  
  
 一个空结果集是与任何其他结果集，只不过它不包含行没有什么不同。 例如，应用程序可以检索结果集的元数据，可以尝试提取行，和必须通过结果集时关闭游标。  
  
 从数据源检索行并将其返回到应用程序的过程称为*提取*。 本部分介绍该过程的基本部分。 有关更高级的主题，例如块和可滚动游标，请参阅[块状游标](../../../odbc/reference/develop-app/block-cursors.md)并[可滚动游标](../../../odbc/reference/develop-app/scrollable-cursors.md)。 有关更新的信息，删除和插入行，请参阅[更新数据概述](../../../odbc/reference/develop-app/updating-data-overview.md)。  
  
 本部分包含以下主题。  
  
-   [是否创建了一个结果集？](../../../odbc/reference/develop-app/was-a-result-set-created.md)  
  
-   [结果集元数据](../../../odbc/reference/develop-app/result-set-metadata.md)  
  
-   [绑定列](../../../odbc/reference/develop-app/binding-columns.md)  
  
-   [提取数据](../../../odbc/reference/develop-app/fetching-data.md)  
  
-   [关闭游标](../../../odbc/reference/develop-app/closing-the-cursor.md)
