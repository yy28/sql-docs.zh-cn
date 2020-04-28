---
title: 互操作性 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306218"
---
# <a name="interoperability"></a>互操作性
*互操作性*是指单个应用程序使用多个不同 dbms 进行操作的能力。 编写通用的可互操作应用程序的需要是导致 ODBC 开发的主要因素之一。 但是，互操作性并不是从 "无法互操作" 到 "完全可互操作" 的简单途径。 路径包含多个分支，每个分支都需要特性、速度、代码复杂性和开发时间之间的权衡。  
  
 编写互操作应用程序的过程如下所示：  
  
1.  确定应用程序是否将使用 ODBC。  
  
2.  选择一级别的互操作性，并确定需要进行哪些权衡才能达到该级别。  
  
3.  编写互操作代码并尽可能完全地测试。  
  
 请注意，互操作性主要是应用程序编写器的域。 驱动程序设计为与单个 DBMS 一起使用，并且根据定义，它们不可互操作。 它们通过在单个 DBMS 上正确实现和公开 ODBC，扮演互操作性角色。  
  
 本部分包含以下主题。  
  
-   [需要 ODBC？](../../../odbc/reference/develop-app/is-odbc-the-answer.md)  
  
-   [选择互操作性的级别](../../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md)  
  
-   [确定目标 DBMS 和驱动程序](../../../odbc/reference/develop-app/determining-the-target-dbmss-and-drivers.md)  
  
-   [考虑使用数据库功能](../../../odbc/reference/develop-app/considering-database-features-to-use.md)  
  
-   [产品周期长度](../../../odbc/reference/develop-app/length-of-the-product-cycle.md)  
  
-   [编写交互式应用程序](../../../odbc/reference/develop-app/writing-an-interoperable-application.md)  
  
-   [测试交互式应用程序](../../../odbc/reference/develop-app/testing-interoperable-applications.md)
