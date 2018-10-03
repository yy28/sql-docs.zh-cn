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
manager: craigg
ms.openlocfilehash: bc5a354aeaf186b4baeabd96e7424939fe463bfb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47777415"
---
# <a name="sqlstatistics-access-driver"></a>SQLStatistics（Access 驱动程序）
> [!NOTE]  
>  本主题提供访问特定于驱动程序信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
|“列”|注释|  
|------------|--------------|  
|TABLE_QUALIFIER|返回 Microsoft Access 数据库文件的路径。<br /><br /> 中不支持模式匹配*szTableQualifier*参数。|  
|TABLE_OWNER|在本专栏中，则返回 NULL，因为不支持所有者名称。|  
|TABLE_NAME|未分隔的表名称。<br /><br /> 中不支持模式匹配*szTableName*参数。|  
|INDEX_QUALIFIER|始终返回 NULL。|  
|INDEX_NAME|索引相关。|  
|TYPE|只有 SQL_TABLE_STAT 或 SQL_INDEX_OTHER 将为类型返回。|  
|SEQ_IN_INDEX|索引相关。|  
|COLUMN_NAME|索引相关。|  
|COLLATION|索引相关。|  
|CARDINALITY|仅返回 Microsoft Access。|  
|PAGES|始终返回 NULL。|  
  
 筛选基于唯一性 ( *fUnique*参数)。 *FAccuracy*参数将被忽略。
