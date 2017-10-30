---
title: "SQL 模块 |Microsoft 文档"
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
- SQL modules [ODBC]
- sending SQL statements to DBMS [ODBC]
- SQL [ODBC], modules
- modules [ODBC]
- SQL statements [ODBC], modules
ms.assetid: 07551472-87ee-4765-951f-1364ed32f0c0
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f37ab932ef230d29a5db23aec920230de0443e37
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sql-modules"></a>SQL 模块
将 SQL 语句发送到 DBMS 的第二个方法是通过模块。 简言之，模块包含一组过程，从宿主编程语言调用。 每个过程包含单个 SQL 语句中，并且数据将通过参数传递到和从过程。  
  
 模块可以看作对象库链接到应用程序代码。 但是，完全过程和应用程序的其余部分如何链接是依赖于实现的。 例如，无法为对象代码编译过程，并将其直接链接到应用程序代码、 无法进行编译和存储上的 DBMS 和调用访问计划标识符放置在应用程序代码中，或无法在运行时对它们进行解释。  
  
 模块的主要优点是它们完全分隔的编程语言中的 SQL 语句。 从理论上讲，它应能更改而无需更改另一个，并只需将它们重新。

