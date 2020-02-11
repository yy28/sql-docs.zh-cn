---
title: SQLPrimaryKeys （Visual FoxPro ODBC 驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLPrimaryKeys function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 8dbe2903-efdc-45e0-a079-9e357c5fd81b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e85e60cde86c9483e69a8c43de14ef64eb914119
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68030703"
---
# <a name="sqlprimarykeys-visual-foxpro-odbc-driver"></a>SQLPrimaryKeys（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含特定于 Visual FoxPro ODBC 驱动程序的信息。 有关此函数的常规信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)中的相应主题。  
  
 支持：完全  
  
 ODBC API 一致性：级别2  
  
 返回构成表的主键的列名称。 **SQLPrimaryKeys**的 VISUAL FoxPro ODBC 驱动程序实现的行为如下所示：  
  
-   忽略*szTableOwner*和*cbTableOwner*参数。  
  
-   仅适用于[数据库](../../odbc/microsoft/visual-foxpro-terminology.md)数据源。 如果数据源是[可用表](../../odbc/microsoft/visual-foxpro-terminology.md)的目录，则驱动程序将返回错误 "驱动程序不支持此函数"。  
  
 有关详细信息，请参阅*ODBC 程序员参考*中的[SQLPrimaryKeys](../../odbc/reference/syntax/sqlprimarykeys-function.md) 。
