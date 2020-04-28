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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 83631d22bd07017c4eba8f6af171443ab8c76d9c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301542"
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
