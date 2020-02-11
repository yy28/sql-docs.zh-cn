---
title: SQLBindCol （Visual FoxPro ODBC 驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBindCol function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 984d6605-39ba-4d33-ac94-22625bfa6107
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 706677b71d1243baac0ca576bb3087d50abb6796
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68098301"
---
# <a name="sqlbindcol-visual-foxpro-odbc-driver"></a>SQLBindCol（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含特定于 Visual FoxPro ODBC 驱动程序的信息。 有关此函数的常规信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)中的相应主题。  
  
 支持：完全  
  
 ODBC API 一致性：核心级别  
  
 为结果列分配存储空间，并指定结果的类型。 调用[SQLFetch](../../odbc/microsoft/sqlfetch-visual-foxpro-odbc-driver.md)或[SQLExtendedFetch](../../odbc/microsoft/sqlextendedfetch-visual-foxpro-odbc-driver.md)时，驱动程序将为分配的位置中的所有绑定列放置数据。 有关 ODBC 和 Visual FoxPro 数据类型之间的映射，请参阅[SQLGetTypeInfo](../../odbc/microsoft/sqlgettypeinfo-visual-foxpro-odbc-driver.md) 。  
  
 有关详细信息，请参阅*ODBC 程序员参考*中的[SQLBindCol](../../odbc/reference/syntax/sqlbindcol-function.md) 。
