---
title: SQLPrimaryKeys （Visual FoxPro ODBC 驱动程序） |Microsoft 文档
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
ms.topic: article
helpviewer_keywords:
- SQLPrimaryKeys function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 8dbe2903-efdc-45e0-a079-9e357c5fd81b
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 722350a83060a37eecadaf091be7655164d868d5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sqlprimarykeys-visual-foxpro-odbc-driver"></a>SQLPrimaryKeys （Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含 Visual FoxPro ODBC 驱动程序相关的信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支持： 完整  
  
 ODBC API 一致性： 级别 2  
  
 返回构成表的主键的列名称。 Visual FoxPro ODBC 驱动程序实现**SQLPrimaryKeys**行为，如下所示：  
  
-   将忽略*szTableOwner*和*cbTableOwner*自变量。  
  
-   仅适用于数据源[数据库](../../odbc/microsoft/visual-foxpro-terminology.md)。 该驱动程序将返回错误"驱动程序不支持此函数"如果数据源是一个目录的[释放表](../../odbc/microsoft/visual-foxpro-terminology.md)。  
  
 有关详细信息，请参阅[SQLPrimaryKeys](../../odbc/reference/syntax/sqlprimarykeys-function.md)中*ODBC 程序员参考*。
