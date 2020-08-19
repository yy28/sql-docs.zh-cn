---
description: SQLStatistics（dBASE 驱动程序）
title: SQLStatistics (dBASE 驱动程序) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLStatistics function [ODBC], dBASE Driver
- DBase driver [ODBC], SQLStatistics
ms.assetid: 631cec1b-66b7-4103-b9a7-ffd81da3c442
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9285f78bbafb7594e3a9cbab2845cedeff0c1af9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421561"
---
# <a name="sqlstatistics-dbase-driver"></a>SQLStatistics（dBASE 驱动程序）
> [!NOTE]  
>  本主题提供了特定于 dBASE 驱动程序的信息。 有关此函数的常规信息，请参阅 [ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)中的相应主题。  
  
|列|注释|  
|------------|--------------|  
|TABLE_QUALIFIER|目录的路径。<br /><br /> *SzTableQualifier*参数中不支持模式匹配。|  
|TABLE_OWNER|由于不支持所有者名称，因此在此列中返回 NULL。|  
|TABLE_NAME|Get-content 表名称。<br /><br /> *SzTableName*参数中不支持模式匹配。|  
|INDEX_QUALIFIER|始终返回 NULL。|  
|INDEX_NAME|与索引相关。|  
|TYPE|只会为类型返回 SQL_TABLE_STAT 或 SQL_INDEX_OTHER。|  
|SEQ_IN_INDEX|与索引相关。|  
|COLUMN_NAME|与索引相关。|  
|COLLATION|与索引相关。|  
|PAGES|始终返回 NULL。|  
  
 筛选基于 *fUnique* 参数) 的唯一性 (。 忽略 *fAccuracy* 参数。
