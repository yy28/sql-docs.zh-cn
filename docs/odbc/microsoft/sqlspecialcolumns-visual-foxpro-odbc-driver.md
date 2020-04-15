---
title: SQL 特殊柱（可视化福克斯 Pro ODBC 驱动程序） |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 96b439674c8bda3494b4cefd0c1118602b537cd0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299377"
---
# <a name="sqlspecialcolumns-visual-foxpro-odbc-driver"></a>SQLSpecialColumns（Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含 Visual FoxPro ODBC 特定于驱动程序的信息。 有关此功能的一般信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)下的相应主题。  
  
 支持： 完整  
  
 ODBC API 符合性：1 级  
  
 检索唯一标识表中行的最佳列集。  
  
 Visual FoxPro ODBC 驱动程序返回构成 FoxPro 表主键的列。 （请参阅[SQL 主键](../../odbc/microsoft/sqlprimarykeys-visual-foxpro-odbc-driver.md)。如果使用*fColType*设置为 SQL_ROWVER调用，则不返回任何列。 **SQL特殊列只**对[数据库](../../odbc/microsoft/visual-foxpro-terminology.md)的数据源有效。  
  
 有关详细信息，请参阅*ODBC 程序员参考*中的[SQL 特殊列。](../../odbc/reference/syntax/sqlspecialcolumns-function.md)
