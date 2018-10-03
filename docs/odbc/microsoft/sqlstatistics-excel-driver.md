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
manager: craigg
ms.openlocfilehash: 044ea7e2c536685afef3534eacb5745fb33edf49
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47619405"
---
# <a name="sqlstatistics-excel-driver"></a>SQLStatistics（Excel 驱动程序）
> [!NOTE]  
>  本主题提供了特定于 Excel 驱动程序的信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
|“列”|注释|  
|------------|--------------|  
|TABLE_QUALIFIER|目录的路径。<br /><br /> 中不支持模式匹配*szTableQualifier*参数。|  
|TABLE_OWNER|在本专栏中则返回 NULL，因为不支持所有者名称。|  
|TABLE_NAME|未分隔的表名称。<br /><br /> 中不支持模式匹配*szTableName*参数。|  
|INDEX_QUALIFIER|始终返回 NULL。|  
|INDEX_NAME|索引相关。|  
|TYPE|只有 SQL_TABLE_STAT 或 SQL_INDEX_OTHER 将为类型返回。|  
|SEQ_IN_INDEX|索引相关。|  
|COLUMN_NAME|索引相关。|  
|COLLATION|索引相关。|  
|PAGES|始终返回 NULL。|  
  
 筛选基于唯一性 ( *fUnique*参数)。 *FAccuracy*参数将被忽略。
