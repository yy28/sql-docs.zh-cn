---
title: 块游标、 可滚动游标和向后兼容性 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], backward compatibility
- compatibility [ODBC], cursors
- backward compatibility [ODBC], cursors
- block cursors [ODBC]
ms.assetid: d9d271f6-d2d9-49b9-a365-4909ca06caae
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d3896473a1fa08f769f13d94bd1d81f373cf67c0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63026600"
---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility"></a>块游标、可滚动游标和后向兼容性
这两者的存在**SQLFetchScroll**并**SQLExtendedFetch**表示首先清除拆分 ODBC 之间应用程序编程接口 (API)，这是组的函数中服务提供程序接口 (SPI)，这是组的函数和应用程序调用，该驱动程序实现。 此拆分是必需的以便 ODBC 3。*x*，使用**SQLFetchScroll**，与标准 bealigned，也是与 ODBC 2 兼容。*x*，使用该**SQLExtendedFetch**。  
  
 ODBC 3 *.x* API，这是组函数的应用程序调用，包括**SQLFetchScroll**和相关的语句属性。 ODBC 3 *.x* SPI，这是一组函数的驱动程序实现，包括**SQLFetchScroll**， **SQLExtendedFetch**，和相关的语句属性。 由于 ODBC 不正式实施之间的 API 和 SPI 的划分，所以有可能对于 ODBC 3 *.x*应用程序可以调用**SQLExtendedFetch**和相关的语句属性。 但是，没有针对 ODBC 3 理由 *.x*应用程序来执行此操作。 有关 Api 和 Spi 的详细信息，请参阅简介[ODBC 体系结构](../../../odbc/reference/odbc-architecture.md)。  
  
 有关哪些函数和语句属性 ODBC 3。*x*应用程序应使用包含块，但可滚动游标，请参阅[块游标、 可滚动游标和 ODBC 3.x 应用程序的向后兼容性](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)。  
  
 本部分包含以下主题。  
  
-   [驱动程序管理器的用途](../../../odbc/reference/appendixes/what-the-driver-manager-does.md)  
  
-   [驱动程序的用途](../../../odbc/reference/appendixes/what-the-driver-does.md)
