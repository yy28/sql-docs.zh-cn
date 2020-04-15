---
title: 块光标、可滚动光标和向后兼容性 |微软文档
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
ms.openlocfilehash: fe24362f1a49577a7fb494f768947080d0ab6e9e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292307"
---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility"></a>块游标、可滚动游标和后向兼容性
**SQLFetchScroll**和**SQLExtendedFetch**的存在代表了在 ODBC 中，应用程序编程接口 （API） 和服务提供者接口 （SPI） 之间的第一个明确拆分，这是驱动程序实现的函数集。 这种拆分是必要的，以便使用**SQLFetchScroll**的 ODBC *3.x*与标准保持一致，并且与使用**SQLAt2.x**的 ODBC *2.x*兼容 。  
  
 ODBC *3.x* API 是应用程序调用的功能集，包括**SQLFetchScroll**和相关语句属性。 ODBC *3.x* SPI 是驱动程序实现的函数集，包括**SQLFetchScroll、SQL****扩展获取**和相关语句属性。 由于 ODBC 未正式强制 API 和 SPI 之间的此拆分，因此 ODBC *3.x*应用程序可以调用**SQLExtendedFetch**和相关语句属性。 但是，ODBC *3.x*应用程序没有理由这样做。 有关 API 和 API 的详细信息，请参阅[ODBC 体系结构](../../../odbc/reference/odbc-architecture.md)的简介。  
  
 有关 ODBC *3.x*应用程序应使用哪些函数和语句属性的信息，请参阅[块光标、可滚动光标和 ODBC 3.x 应用程序的向后兼容性](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md)。  
  
 本部分包含以下主题。  
  
-   [驱动程序管理器的用途](../../../odbc/reference/appendixes/what-the-driver-manager-does.md)  
  
-   [驱动程序的用途](../../../odbc/reference/appendixes/what-the-driver-does.md)
