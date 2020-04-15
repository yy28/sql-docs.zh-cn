---
title: SQL统计（访问驱动程序） |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLStatistics
- SQLStatistics function [ODBC], Access Driver
ms.assetid: 6117ac77-1020-4f0c-8eed-e671c34c1f21
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f75f41bf63cbf224772955effa0f120b5d384111
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299357"
---
# <a name="sqlstatistics-access-driver"></a>SQLStatistics（Access 驱动程序）
> [!NOTE]  
>  本主题提供特定于访问驱动程序的信息。 有关此功能的一般信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)下的相应主题。  
  
|列|注释|  
|------------|--------------|  
|TABLE_QUALIFIER|返回数据库文件的路径以用于 Microsoft Access。<br /><br /> *szTable限定符*参数不支持模式匹配。|  
|TABLE_OWNER|NULL 在此列中返回，因为不支持所有者名称。|  
|TABLE_NAME|未限制的表名称。<br /><br /> *szTableName*参数不支持模式匹配。|  
|INDEX_QUALIFIER|NULL 始终返回。|  
|INDEX_NAME|依赖于索引。|  
|TYPE|只有SQL_TABLE_STAT或SQL_INDEX_OTHER将返回 TYPE。|  
|SEQ_IN_INDEX|依赖于索引。|  
|COLUMN_NAME|依赖于索引。|  
|COLLATION|依赖于索引。|  
|CARDINALITY|仅为 Microsoft 访问返回。|  
|PAGES|NULL 始终返回。|  
  
 筛选基于唯一性 *（f唯一*参数）。 *fAccuracy*参数将被忽略。
