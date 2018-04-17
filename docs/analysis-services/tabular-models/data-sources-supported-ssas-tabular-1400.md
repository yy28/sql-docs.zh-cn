---
title: 在 SQL Server Analysis Services 表格 1400年模型中支持的数据源 |Microsoft 文档
ms.date: 03/26/2018
ms.prod: analysis-services
ms.suite: pro-bi
ms.topic: article
ms.assetid: ''
author: Minewiskan
ms.author: owend
manager: kfile
monikerRange: '>= sql-analysis-services-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: c32b715ac73fd69e63bad8487950ff1e4df003c9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="data-sources-supported-in-sql-server-analysis-services-tabular-1400-models"></a>数据源中支持 SQL Server Analysis Services 表格 1400年模型

[!INCLUDE[ssas-appliesto-sql2017](../../includes/ssas-appliesto-sql2017.md)]

本文介绍可与 SQL Server Analysis Services (SSAS) 1400年兼容级别的表格模型使用的数据源的类型。 

SSAS 在 1200年和较低的兼容性级别的表格模型，请参阅[支持 SQL Server Analysis Services 表格 1200年模型中的数据源](data-sources-supported-ssas-tabular.md)。

Azure Analysis Services，请参阅[Azure Analysis Services 中支持的数据源](https://docs.microsoft.com/azure/analysis-services/analysis-services-datasource)。


## <a name="cloud-data-sources"></a>云数据源

|Azure 数据源  |内存中  |DirectQuery  |
|---------|---------|---------|
|Azure SQL Database     |   是      |    是      |
|Azure SQL 数据仓库     |   是      |   是       |
|Azure Blob 存储     |   是       |    否      |
|Azure 表存储    |   是       |    否      |
|Azure Cosmos DB      |  是        |  否        |
|Azure 数据湖存储     |   是       |    否      |
|Azure HDInsight HDFS     |     是     |   否       |
|Azure HDInsight Spark (Beta)     |   是       |   否       |
||||

**提供程序**   
内存中和连接到 Azure 的数据源的 DirectQuery 模型用于 SQL Server.NET Framework 数据提供程序。

## <a name="on-premises-data-sources"></a>本地数据源

### <a name="supported-by-in-memory-and-directquery-models"></a>支持内存中和 DirectQuery 模型

|数据源 | 内存中提供程序 | DirectQuery 提供程序 |
|  --- | --- | --- |
| SQL Server |SQL Server Native Client 11.0，Microsoft OLE DB Provider for SQL Server、 SQL Server 的.NET Framework 数据提供程序 | 用于 SQL Server 的 .NET Framework 数据访问接口 |
| SQL Server 数据仓库 |SQL Server Native Client 11.0，Microsoft OLE DB Provider for SQL Server、 SQL Server 的.NET Framework 数据提供程序 | 用于 SQL Server 的 .NET Framework 数据访问接口 |
| Oracle |Microsoft OLE DB Provider for Oracle，用于.NET 的 Oracle 数据提供程序 |用于.NET 的 oracle 数据提供程序 | |
| Teradata |OLE DB Provider for Teradata，适用于.NET 的 Teradata 数据提供程序 |用于.NET Teradata 数据提供程序 | |
| | | |

> [!NOTE]
> 对于内存中模型，OLE DB 提供程序可以提供更好的性能大规模数据。 在选择相同的数据源的不同访问接口时，请首先尝试 OLE DB 访问接口。  

### <a name="supported-by-in-memory-models-only"></a>内存中模型仅支持

|数据库  |
|---------|---------|---------|
|Access 数据库     | 
|SQL Server Analysis Services     | 
|IBM Informix (beta) | 
|JSON 文档     | 
|从二进制文件的行     | 
|MySQL 数据库     | 
|PostgreSQL 数据库    | 是 | 否
|SAP HANA   | 是 | 否
|SAP Business Warehouse    | 是 | 否
|Sybase 数据库     | 是 | 否
|||

|文件  |  
|---------|---------|
|Excel 工作簿     |
|文件夹     | 
|JSON | 
|Text/CSV    | 
|XML 表    | 
|||

|在线服务  |  
|---------|---------|
|Dynamics 365      |
|Exhange 联机     |
|Saleforce 对象    | 
|Salesforce 报表     |
|SharePoint Online 列表     |
|||

|其他  |  
|---------|---------|
|Active Directory      | 
|Exhange     |  
|OData 数据源     | 
|ODBC 查询     | 
|OLE DB  | 
|SharePoint 列表 | 
|||

## <a name="see-also"></a>另请参阅

[数据源支持在 SQL Server Analysis Services 中表格 1200年模型](data-sources-supported-ssas-tabular.md)

[在 Azure Analysis Services 中受支持的数据源](https://docs.microsoft.com/azure/analysis-services/analysis-services-datasource)   
