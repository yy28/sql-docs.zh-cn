---
title: SQLStatistics （Access 驱动程序） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 523f44924858af182e953aa1ce2b72e20cf97a45
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68047077"
---
# <a name="sqlstatistics-access-driver"></a>SQLStatistics（Access 驱动程序）
> [!NOTE]  
>  本主题提供特定于访问驱动程序的信息。 有关此函数的常规信息，请参阅[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)中的相应主题。  
  
|列|注释|  
|------------|--------------|  
|TABLE_QUALIFIER|为 Microsoft Access 返回数据库文件的路径。<br /><br /> *SzTableQualifier*参数中不支持模式匹配。|  
|TABLE_OWNER|由于不支持所有者名称，因此在此列中返回 NULL。|  
|TABLE_NAME|Get-content 表名称。<br /><br /> *SzTableName*参数中不支持模式匹配。|  
|INDEX_QUALIFIER|始终返回 NULL。|  
|INDEX_NAME|与索引相关。|  
|类型|只会为类型返回 SQL_TABLE_STAT 或 SQL_INDEX_OTHER。|  
|SEQ_IN_INDEX|与索引相关。|  
|COLUMN_NAME|与索引相关。|  
|COLLATION|与索引相关。|  
|CARDINALITY|仅为 Microsoft Access 返回。|  
|PAGES|始终返回 NULL。|  
  
 筛选基于唯一性（ *fUnique*参数）。 忽略*fAccuracy*参数。
