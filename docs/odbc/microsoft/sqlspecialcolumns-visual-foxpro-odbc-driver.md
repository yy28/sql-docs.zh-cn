---
title: SQLSpecialColumns （Visual FoxPro ODBC 驱动程序） |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLSpecialColumns function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: b72a978d-6a60-475a-b7d9-c424d77bbe30
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4c9ebafa51d44f8c9b0ee43a118867c6410b1099
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sqlspecialcolumns-visual-foxpro-odbc-driver"></a>SQLSpecialColumns （Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含 Visual FoxPro ODBC 驱动程序相关的信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支持： 完整  
  
 ODBC API 一致性： 级别 1  
  
 检索列的最佳唯一标识表中的行集。  
  
 Visual FoxPro ODBC 驱动程序返回构成 FoxPro 表的主键的列。 (请参阅[SQLPrimaryKeys](../../odbc/microsoft/sqlprimarykeys-visual-foxpro-odbc-driver.md)。)如果使用调用*fColType*设置为 SQL_ROWVER，返回没有列。 **SQLSpecialColumns**仅适用于数据源[数据库](../../odbc/microsoft/visual-foxpro-terminology.md)。  
  
 有关详细信息，请参阅[SQLSpecialColumns](../../odbc/reference/syntax/sqlspecialcolumns-function.md)中*ODBC 程序员参考*。
