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
manager: craigg
ms.openlocfilehash: 3eeafa338fea31741609e6f9a9b32a4128ebd87d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62636326"
---
# <a name="sqlprimarykeys-visual-foxpro-odbc-driver"></a>SQLPrimaryKeys（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含 Visual FoxPro ODBC 驱动程序特定信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支持：完全  
  
 ODBC API 一致性：级别 2  
  
 返回包含表的主键的列名称。 Visual FoxPro ODBC 驱动程序实现**SQLPrimaryKeys**行为，如下所示：  
  
-   将忽略*szTableOwner*并*cbTableOwner*参数。  
  
-   仅适用于数据源[数据库](../../odbc/microsoft/visual-foxpro-terminology.md)。 该驱动程序将返回错误"驱动程序不支持此函数"的目录数据源是否[免费表](../../odbc/microsoft/visual-foxpro-terminology.md)。  
  
 有关详细信息，请参阅[SQLPrimaryKeys](../../odbc/reference/syntax/sqlprimarykeys-function.md)中*ODBC 程序员参考*。
