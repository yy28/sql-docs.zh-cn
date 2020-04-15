---
title: SQL统计（文本文件驱动程序） |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], SQLStatistics
- SQLStatistics function [ODBC], Text File Driver
ms.assetid: 311afc01-d656-425f-be43-4a8e7cbc9a97
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 76b9810236b4ec415f8abb8ecefca748c13b51c8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299307"
---
# <a name="sqlstatistics-text-file-driver"></a>SQLStatistics（文本文件驱动程序）
> [!NOTE]  
>  本主题提供特定于文本文件驱动程序的信息。 有关此功能的一般信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)下的相应主题。  
  
|列|注释|  
|------------|--------------|  
|TABLE_QUALIFIER|目录的路径。<br /><br /> *szTable限定符*参数不支持模式匹配。|  
|TABLE_OWNER|由于不支持所有者名称，因此在此列中返回 NULL。|  
|TABLE_NAME|未限制的表名称。<br /><br /> *szTableName*参数不支持模式匹配。|  
|INDEX_QUALIFIER|NULL 始终返回。|  
|INDEX_NAME|依赖于索引。|  
|TYPE|只有SQL_TABLE_STAT或SQL_INDEX_OTHER将返回 TYPE。|  
|SEQ_IN_INDEX|依赖于索引。|  
|COLUMN_NAME|依赖于索引。|  
|COLLATION|依赖于索引。|  
|PAGES|NULL 始终返回。|  
  
 筛选基于唯一性 *（f唯一*参数）。 *fAccuracy*参数将被忽略。
