---
title: SQLAllocConnect（视觉福克斯Pro ODBC驱动程序） |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLAllocConnect function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 70d48b12-def5-475c-b8e1-654a55fdfe0f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6e5fa95bb958431f717c073673e0b4ad93056e62
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300658"
---
# <a name="sqlallocconnect-visual-foxpro-odbc-driver"></a>SQLAllocConnect（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含 Visual FoxPro ODBC 特定于驱动程序的信息。 有关此功能的一般信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)下的相应主题。  
  
 支持： 完整  
  
 ODBC API 一致性：核心级别  
  
 在*henv*标识的环境中为连接句柄*hdbc*分配内存。 驱动程序管理器处理此调用，并在调用**SQLConnect、SQLBrowseConnect**或[SQLConnect](../../odbc/microsoft/sqlconnect-visual-foxpro-odbc-driver.md) [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)时调用驱动程序的**SQLAllocConnect。**  
  
 有关详细信息，请参阅*ODBC 程序员参考*中的[SQLAllocConnect。](../../odbc/reference/syntax/sqlallocconnect-function.md)
