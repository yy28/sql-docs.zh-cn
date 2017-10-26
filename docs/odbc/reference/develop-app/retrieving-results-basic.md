---
title: "检索结果 (Basic) |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- result sets [ODBC], about result sets
- data sources [ODBC], result sets
- empty result sets [ODBC]
ms.assetid: 052870e3-3f3f-4f07-91da-b649348225f4
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 05a58b18fab1fe40220b20e8b18849acc4de11a9
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="retrieving-results-basic"></a>检索结果 (Basic)
A*结果集*是一组与某些条件匹配的数据源上的行。 它是概念的表中时得到的查询以及在表格窗体中可用的应用程序。 **选择**语句、 目录函数和某些过程创建结果集。 在下面的示例中，第一个 SQL 语句将创建一个结果集，其中包含的所有行和 Orders 表中的所有列和第二个 SQL 语句将创建包含 OrderID、 销售人员，和状态订单表中的行的列的结果集在其中状态是已打开：  
  
```  
SELECT * FROM Orders  
SELECT OrderID, SalesPerson, Status FROM Orders WHERE Status = 'OPEN'  
```  
  
 结果集可以为空，这是不同于根本设置任何结果。 例如，以下 SQL 语句创建一个空的结果集：  
  
```  
SELECT * FROM Orders WHERE 1 = 2  
```  
  
 空结果集是与任何其他结果集，只不过它具有任何行没有什么不同。 例如，应用程序可以检索结果集的元数据，可以尝试提取行，和必须通过结果集时关闭游标。  
  
 从数据源中检索行并将它们返回到应用程序的过程被称为*提取*。 本部分介绍该进程的基本组成部分。 有关更高级主题，例如块和可滚动游标，请参阅[块状游标](../../../odbc/reference/develop-app/block-cursors.md)和[可滚动游标](../../../odbc/reference/develop-app/scrollable-cursors.md)。 删除和插入行，有关更新的信息，请参阅[更新数据概述](../../../odbc/reference/develop-app/updating-data-overview.md)。  
  
 本部分包含以下主题。  
  
-   [是一个结果集，创建？](../../../odbc/reference/develop-app/was-a-result-set-created.md)  
  
-   [结果集元数据](../../../odbc/reference/develop-app/result-set-metadata.md)  
  
-   [绑定列](../../../odbc/reference/develop-app/binding-columns.md)  
  
-   [提取数据](../../../odbc/reference/develop-app/fetching-data.md)  
  
-   [关闭游标](../../../odbc/reference/develop-app/closing-the-cursor.md)

