---
title: "PolyBase 受版本控制的功能摘要 | Microsoft Docs"
ms.custom: 
ms.date: 08/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: polybase
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6591994d-6109-4285-9c5b-ecb355f8a111
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ff2d8cb28ff4d1ae4960d183ce73524ecf24d7d3
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2018
---
# <a name="polybase-versioned-feature-summary"></a>PolyBase 受版本控制的功能摘要
[!INCLUDE[appliesto-ss2016-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-all-md.md)]
可用于 SQL Server 产品和服务的 PolyBase 功能摘要。  
  
## <a name="feature-summary-for-product-releases"></a>产品版本的功能摘要  
 此表概述了 PolyBase 的主要功能以及提供这些功能的产品。  
  
||||||
|-|-|-|-|-|   
|**功能**|**SQL Server 2016**|**Azure SQL 数据库**|**Azure SQL 数据仓库**|**并行数据仓库**| 
|查询 Hadoop 数据和 [!INCLUDE[tsql](../../includes/tsql-md.md)]|是|否|否|是|
|从 Hadoop 导入数据|是|否|否|是|
|导出数据到 Hadoop  |是|否|否| 是|
|查询、从 HDInsights 导入、导出自 HDInsight |否|否|否|否
|将查询计算下推到 Hadoop|是|否|否|是|  
|从 Azure blob 存储导入数据|是|否|是|是| 
|导出数据到 Azure blob 存储|是|否|是|是|  
|从 Azure Data Lake Store 导入数据|否|否|是|否|    
|从 Azure Data Lake Store 导出数据|否|否|是|否|
|从 Microsoft 的 BI 工具运行 PolyBase Queries|是|否|是|是|   


## <a name="pushdown-computation-supported-t-sql-operators"></a>下推计算支持 T-SQL 运算符
在 SQL Server 和 APS 中，不是所有 T-SQL 运算符都可下推到 hadoop 群集。 下表列出了所有支持的运算符和不支持运算符的子集。 

||||
|-|-|-| 
|运算符类型|可推送到 Hadoop|可推送到 Blob 存储|
|列投影|是|否|
|谓词|是|否|
|聚合|部分|否|
|外部表之间的联接|否|否|
|外部表和本地表之间的联接|否|否|
|排序|否|否|

部分聚合意味着一旦数据到达 SQL Server，必须立即发生最终聚合，但是一部分聚合发生在 Hadoop 中。 这是在大规模并行处理系统中计算聚合的一种常见方法。  
## <a name="see-also"></a>另请参阅  
 [PolyBase 指南](../../relational-databases/polybase/polybase-guide.md)  
  
  
