---
title: 互操作性 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC]
- interoperability [ODBC], about interoperability
ms.assetid: 43b7c849-9d59-4002-9977-9e2c8730b859
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 31b20a696c601ff91c591e4c717f468beca34e36
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306218"
---
# <a name="interoperability"></a>互操作性
*互操作性*是单个应用程序使用许多不同的 DBMS 运行的能力。 编写通用、可互操作的应用程序是导致 ODBC 开发的主要因素之一。 但是，互操作性不是从"不可互操作"到"完全可互操作"的简单路径。 路径具有许多分支，每个分支都需要在功能、速度、代码复杂性和开发时间之间进行权衡。  
  
 编写可互操作的应用程序的过程遵循几个步骤：  
  
1.  确定应用程序是否将使用 ODBC。  
  
2.  选择互操作性级别，并决定达到该级别所需的权衡。  
  
3.  编写可互操作的代码并尽可能完整地测试它。  
  
 需要注意的是，互操作性主要是应用程序编写器的域。 驱动程序设计为使用单个 DBMS，并且根据定义，它们不可互操作。 通过在单个 DBMS 上正确实现和公开 ODBC，它们在互操作性方面发挥着作用。  
  
 本部分包含以下主题。  
  
-   [需要 ODBC？](../../../odbc/reference/develop-app/is-odbc-the-answer.md)  
  
-   [选择互操作性的级别](../../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md)  
  
-   [确定目标 DBMS 和驱动程序](../../../odbc/reference/develop-app/determining-the-target-dbmss-and-drivers.md)  
  
-   [考虑使用数据库功能](../../../odbc/reference/develop-app/considering-database-features-to-use.md)  
  
-   [产品周期长度](../../../odbc/reference/develop-app/length-of-the-product-cycle.md)  
  
-   [编写交互式应用程序](../../../odbc/reference/develop-app/writing-an-interoperable-application.md)  
  
-   [测试交互式应用程序](../../../odbc/reference/develop-app/testing-interoperable-applications.md)
