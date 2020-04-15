---
title: SQL 主键（可视化福克斯 Pro ODBC 驱动程序） |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301542"
---
# <a name="sqlprimarykeys-visual-foxpro-odbc-driver"></a>SQLPrimaryKeys（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含 Visual FoxPro ODBC 特定于驱动程序的信息。 有关此功能的一般信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)下的相应主题。  
  
 支持： 完整  
  
 ODBC API 符合性：2 级  
  
 返回构成表主键的列名称。 **SQL主要密钥**的可视化 FoxPro ODBC 驱动程序实现如下：  
  
-   忽略*szTable 所有者*和*cbTableOwner 参数*。  
  
-   仅适用于[数据库](../../odbc/microsoft/visual-foxpro-terminology.md)的数据源。 如果数据源是[可用表](../../odbc/microsoft/visual-foxpro-terminology.md)的目录，驱动程序将返回错误"驱动程序不支持此函数"。  
  
 有关详细信息，请参阅*ODBC 程序员参考*中的[SQL 主要键](../../odbc/reference/syntax/sqlprimarykeys-function.md)。
