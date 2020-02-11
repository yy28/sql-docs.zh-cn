---
title: SQLStatistics （Excel 驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Excel driver [ODBC], SQLStatistics
- SQLStatistics function [ODBC], Excel Driver
ms.assetid: 02506664-8dcc-4bd0-a8bb-d49fcbdd5722
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1c36d68f42b9b7f76310c453d704c6815ee6de22
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68132466"
---
# <a name="sqlstatistics-excel-driver"></a>SQLStatistics（Excel 驱动程序）
> [!NOTE]  
>  本主题提供了特定于 Excel 驱动程序的信息。 有关此函数的常规信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)中的相应主题。  
  
|列|注释|  
|------------|--------------|  
|TABLE_QUALIFIER|目录的路径。<br /><br /> *SzTableQualifier*参数中不支持模式匹配。|  
|TABLE_OWNER|由于不支持所有者名称，因此在此列中返回 NULL。|  
|TABLE_NAME|Get-content 表名称。<br /><br /> *SzTableName*参数中不支持模式匹配。|  
|INDEX_QUALIFIER|始终返回 NULL。|  
|INDEX_NAME|与索引相关。|  
|类型|只会为类型返回 SQL_TABLE_STAT 或 SQL_INDEX_OTHER。|  
|SEQ_IN_INDEX|与索引相关。|  
|COLUMN_NAME|与索引相关。|  
|COLLATION|与索引相关。|  
|PAGES|始终返回 NULL。|  
  
 筛选基于唯一性（ *fUnique*参数）。 忽略*fAccuracy*参数。
