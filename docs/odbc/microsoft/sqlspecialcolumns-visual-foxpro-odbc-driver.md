---
title: SQLSpecialColumns （Visual FoxPro ODBC 驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSpecialColumns function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: b72a978d-6a60-475a-b7d9-c424d77bbe30
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7c4095448b8a9068dad3c4df1c28065e7cffbd67
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47721140"
---
# <a name="sqlspecialcolumns-visual-foxpro-odbc-driver"></a>SQLSpecialColumns（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含 Visual FoxPro ODBC 驱动程序特定信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支持： 完整  
  
 ODBC API 一致性： 级别 1  
  
 检索最佳列集的唯一标识表中的行。  
  
 Visual FoxPro ODBC 驱动程序返回构成 FoxPro 表的主键的列。 (请参阅[SQLPrimaryKeys](../../odbc/microsoft/sqlprimarykeys-visual-foxpro-odbc-driver.md)。)如果使用调用*fColType*设置为 SQL_ROWVER，会返回任何列。 **SQLSpecialColumns**仅适用于数据源[数据库](../../odbc/microsoft/visual-foxpro-terminology.md)。  
  
 有关详细信息，请参阅[SQLSpecialColumns](../../odbc/reference/syntax/sqlspecialcolumns-function.md)中*ODBC 程序员参考*。
