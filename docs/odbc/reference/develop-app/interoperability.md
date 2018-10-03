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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8d5e4fbee458bec88461d3e2945a466c848d3345
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47794115"
---
# <a name="interoperability"></a>互操作性
*互操作性*是单个应用程序的许多不同的 Dbms 的能力。 需要编写通用、 可互操作的应用程序是领先的开发的 ODBC 的主要因素之一。 但是，互操作性不是简单的路径，然后从"不可互操作"到"完全可互操作。" 路径有许多分支，并且每个需要功能、 速度、 代码复杂性和开发时间之间的权衡。  
  
 编写可互操作应用程序的过程包括多个步骤：  
  
1.  确定应用程序是否将使用 ODBC。  
  
2.  选择互操作性，并确定哪些权衡达到该级别所需的级别。  
  
3.  编写可互操作代码，并尽可能完全对其进行测试。  
  
 应注意的互操作性是主要的应用程序编写器的域。 驱动程序用于处理单个 DBMS，并根据定义，不是可互操作。 它们通过正确实现，并通过单个 DBMS 公开 ODBC 互操作性中扮演角色。  
  
 本部分包含以下主题。  
  
-   [需要 ODBC？](../../../odbc/reference/develop-app/is-odbc-the-answer.md)  
  
-   [选择互操作性的级别](../../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md)  
  
-   [确定目标 DBMS 和驱动程序](../../../odbc/reference/develop-app/determining-the-target-dbmss-and-drivers.md)  
  
-   [考虑使用数据库功能](../../../odbc/reference/develop-app/considering-database-features-to-use.md)  
  
-   [产品周期长度](../../../odbc/reference/develop-app/length-of-the-product-cycle.md)  
  
-   [编写交互式应用程序](../../../odbc/reference/develop-app/writing-an-interoperable-application.md)  
  
-   [测试交互式应用程序](../../../odbc/reference/develop-app/testing-interoperable-applications.md)
