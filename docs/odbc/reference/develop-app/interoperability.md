---
title: "互操作性 |Microsoft 文档"
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
- interoperability [ODBC]
- interoperability [ODBC], about interoperability
ms.assetid: 43b7c849-9d59-4002-9977-9e2c8730b859
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a96949b4ca739e382a547769f496576bf13db8b7
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="interoperability"></a>互操作性
*互操作性*是单个应用程序以运行许多不同 Dbms 的功能。 编写泛型且可互操作应用程序的需求是导致的 ODBC 开发的主要因素之一。 但是，互操作性不是简单的路径，然后从"不可互操作"到"完全可互操作。" 路径具有许多分支，并且每个需要功能、 速度、 代码复杂性和开发时间之间的权衡。  
  
 编写可互操作的应用程序的过程执行几个步骤：  
  
1.  确定应用程序是否将使用 ODBC。  
  
2.  选择的互操作性和决定哪些权衡所需达到该级别的级别。  
  
3.  编写可互操作的代码，并尽可能完全对其进行测试。  
  
 应注意的是互操作性是主要应用程序编写器的域。 驱动程序旨在使用单个 DBMS，并且根据定义，不是可互操作。 它们通过正确实现并通过单个 DBMS 公开 ODBC 互操作性中发挥作用。  
  
 本部分包含以下主题。  
  
-   [答案是 ODBC？](../../../odbc/reference/develop-app/is-odbc-the-answer.md)  
  
-   [选择互操作性的级别](../../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md)  
  
-   [确定目标 Dbms 和驱动程序](../../../odbc/reference/develop-app/determining-the-target-dbmss-and-drivers.md)  
  
-   [考虑到使用的数据库功能](../../../odbc/reference/develop-app/considering-database-features-to-use.md)  
  
-   [在产品周期的长度](../../../odbc/reference/develop-app/length-of-the-product-cycle.md)  
  
-   [编写可互操作的应用程序](../../../odbc/reference/develop-app/writing-an-interoperable-application.md)  
  
-   [测试可互操作的应用程序](../../../odbc/reference/develop-app/testing-interoperable-applications.md)
