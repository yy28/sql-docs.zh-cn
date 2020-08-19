---
description: SQLStatistics（Paradox 驱动程序）
title: SQLStatistics (Paradox 驱动程序) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Paradox driver [ODBC], SQLStatistics
- SQLStatistics function [ODBC], Paradox Driver
ms.assetid: 886cab83-d599-4fbc-9c88-e8cb833aac4b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cc76e6d2b076a9188850f9a41124311fd2658814
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421551"
---
# <a name="sqlstatistics-paradox-driver"></a>SQLStatistics（Paradox 驱动程序）
> [!NOTE]  
>  本主题提供了特定于驱动程序的信息。 有关此函数的常规信息，请参阅 [ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)中的相应主题。  
  
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
