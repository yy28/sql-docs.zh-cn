---
title: PolyBase 功能和限制 | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.technology: polybase
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 6591994d-6109-4285-9c5b-ecb355f8a111
author: rothja
ms.author: jroth
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2052b098f0be7ab377cf38a36b896794d3caa07a
ms.sourcegitcommit: 8dccf20d48e8db8fe136c4de6b0a0b408191586b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/09/2018
ms.locfileid: "48874345"
---
# <a name="polybase-features-and-limitations"></a>PolyBase 功能和限制

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

## <a name="known-limitations"></a>已知的限制

PolyBase 具有以下限制：

- 在 SQL Server 中最大行大小（包括可变长度列的全长）不能超过 32 KB，在 Azure SQL 数据仓库中不能超过 1 MB。

- PolyBase 不支持 Hive 0.12+ 数据类型（即 Char()、VarChar()）

- 将数据从 SQL Server 或 Azure SQL 数据仓库导出为 ORC 文件格式时，由于因使用 Java 而导致的内存不足错误，包含大量文本的列可能会被限制为 50 列。 若要解决此问题，请仅导出列的一个子集。

- 无法读取或写入 Hadoop 中的静态加密数据。 这包括 HDFS 加密区域或透明加密。

- 如果已启用 KNOX，则 PolyBase 无法连接 Hortonworks 实例。

- 如果使用事务为 true 的 Hive 表，PolyBase 将无法访问 Hive 表目录中的数据。

<!--SQL Server 2016-->
::: moniker range="= sql-server-2016 || =sqlallproducts-allversions"

- [向 SQL Server 2016 故障转移群集添加节点时，PolyBase 没有安装](https://support.microsoft.com/en-us/help/3173087/fix-polybase-feature-doesn-t-install-when-you-add-a-node-to-a-sql-server-2016-failover-cluster)

::: moniker-end
- 不支持集成身份验证。 目前仅支持用户名和密码。  
- 默认启用加密。 若要禁用加密，必须...（与 thanh 交谈）
- [类型映射限制](polybase-type-mapping.md)


## <a name="security-and-authentication"></a>安全性和身份验证 

## <a name="see-also"></a>另请参阅  

[PolyBase 指南](../../relational-databases/polybase/polybase-guide.md)  
