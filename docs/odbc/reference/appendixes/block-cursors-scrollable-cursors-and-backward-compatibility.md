---
description: 块游标、可滚动游标和后向兼容性
title: 块游标、可滚动游标和后向兼容性 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 46f6d3611b0a55325387f2c7723734500d48af83
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411293"
---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility"></a>块游标、可滚动游标和后向兼容性
**SQLFetchScroll**和**SQLExtendedFetch**的存在都表示 ODBC 中的第一个明确拆分 (API) （应用程序调用的函数集）与服务提供程序接口 (SPI) ，后者是驱动程序实现的函数集。 此拆分是必需*的，因此，odbc 1.x*使用**SQLFetchScroll**、bealigned 和标准，并且还与使用**SQLExtendedFetch***的 odbc 2.x 兼容。*  
  
 *ODBC 2.X* API 是应用程序调用的函数集，包括**SQLFetchScroll**和相关语句属性。 *ODBC 2.X* SPI 是驱动程序实现的一组函数，包括**SQLFetchScroll**、 **SQLExtendedFetch**和相关的语句属性。 由于 ODBC 不会在 API 与 SPI 之间正式强制实现此拆分，因此，ODBC *1.x 应用程序* 可以调用 **SQLExtendedFetch** 和相关的语句属性。 不过 *，ODBC 3.x* 应用程序没有理由执行此操作。 有关 Api 和 SPIs 的详细信息，请参阅 [ODBC 体系结构](../../../odbc/reference/odbc-architecture.md)简介。  
  
 有关 ODBC *1.x 应用程序* 应将哪些函数和语句属性用于块和可滚动游标的信息，请参阅 [Odbc 1.x 应用程序的块游标、可滚动游标和向后兼容性](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)。  
  
 本部分包含以下主题。  
  
-   [驱动程序管理器的用途](../../../odbc/reference/appendixes/what-the-driver-manager-does.md)  
  
-   [驱动程序的用途](../../../odbc/reference/appendixes/what-the-driver-does.md)
