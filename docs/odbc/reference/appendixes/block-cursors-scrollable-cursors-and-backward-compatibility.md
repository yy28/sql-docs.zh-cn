---
title: 阻止游标可滚动游标，向后兼容性 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], backward compatibility
- compatibility [ODBC], cursors
- backward compatibility [ODBC], cursors
- block cursors [ODBC]
ms.assetid: d9d271f6-d2d9-49b9-a365-4909ca06caae
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c22ef4ebf761b647f4b0e6bb8c65ccd3457fe694
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility"></a>块状游标可滚动游标，向后兼容性
同时存在**SQLFetchScroll**和**SQLExtendedFetch**首先清除拆分 ODBC 之间应用程序编程接口 (API)，这是组的函数中的表示应用程序调用和服务提供程序接口 (SPI)，这是函数的一套驱动程序实现。 此拆分是必需的以便 ODBC 3。*x*，它使用**SQLFetchScroll**，与标准 bealigned 并同时符合 ODBC 2。*x*，它使用**SQLExtendedFetch**。  
  
 ODBC 3 *.x* api，该 API 的一套应用程序调用的函数、 包括**SQLFetchScroll**和相关语句属性。 ODBC 3 *.x* SPI，是一组函数的驱动程序实现，包括**SQLFetchScroll**， **SQLExtendedFetch**，以及相关语句属性。 因为 ODBC 不会准确地讲强制 API 和 SPI 之间的这种分割，所以有可能 ODBC 3 *.x*应用程序调用**SQLExtendedFetch**和相关语句属性。 但是，没有没有理由 ODBC 3 *.x*应用程序以执行此操作。 有关 Api 和 Spi 的详细信息，请参阅简介[ODBC 体系结构](../../../odbc/reference/odbc-architecture.md)。  
  
 有关哪些函数和语句属性 ODBC 3。*x*应用程序应使用块和可滚动的光标，请参阅[块状游标可滚动游标，对于 ODBC 3.x 应用程序的向后兼容性](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)。  
  
 本部分包含以下主题。  
  
-   [驱动程序管理器的用途](../../../odbc/reference/appendixes/what-the-driver-manager-does.md)  
  
-   [驱动程序的用途](../../../odbc/reference/appendixes/what-the-driver-does.md)
