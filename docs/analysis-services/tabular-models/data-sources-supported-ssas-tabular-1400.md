---
title: 在 SQL Server Analysis Services 表格 1400年模型中支持的数据源 |Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 856e15e7365128bc79d119afe267334fb8470832
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38041655"
---
# <a name="data-sources-supported-in-sql-server-analysis-services-tabular-1400-models"></a>数据源支持在 SQL Server Analysis Services 中表格 1400年模型

[!INCLUDE[ssas-appliesto-sql2017](../../includes/ssas-appliesto-sql2017.md)]

本文介绍可用于在 1400年兼容级别的 SQL Server Analysis Services (SSAS) 表格模型的数据源的类型。 

SSAS 1200 及更低版本兼容性级别的表格模型，请参阅[支持在 SQL Server Analysis Services 表格 1200年模型中的数据源](data-sources-supported-ssas-tabular.md)。

Azure Analysis Services，请参阅[支持 Azure Analysis Services 中的数据源](https://docs.microsoft.com/azure/analysis-services/analysis-services-datasource)。


## <a name="cloud-data-sources"></a>云数据源

|Azure 数据源  |内存中  |DirectQuery  |
|---------|---------|---------|
|Azure SQL Database     |   是      |    是      |
|Azure SQL 数据仓库     |   是      |   是       |
|Azure Blob 存储     |   是       |    “否”      |
|Azure 表存储    |   是       |    “否”      |
|Azure Cosmos DB      |  是        |  “否”        |
|Azure Data Lake Store     |   是       |    “否”      |
|Azure HDInsight HDFS     |     是     |   “否”       |
|Azure HDInsight Spark （beta 版本）     |   是       |   “否”       |
||||

**提供程序**   
内存中和 DirectQuery 模型连接到 Azure 数据源中使用 SQL Server 的.NET Framework 数据提供程序。

## <a name="on-premises-data-sources"></a>在本地数据源

### <a name="supported-by-in-memory-and-directquery-models"></a>内存中和 DirectQuery 模型支持

|数据源 | 内存中提供程序 | DirectQuery 提供程序 |
|  --- | --- | --- |
| SQL Server |SQL Server Native Client 11.0、 用于 SQL Server 的 Microsoft OLE DB 提供程序、 SQL Server 的.NET Framework 数据提供程序 | 用于 SQL Server 的 .NET Framework 数据访问接口 |
| SQL Server 数据仓库 |SQL Server Native Client 11.0、 用于 SQL Server 的 Microsoft OLE DB 提供程序、 SQL Server 的.NET Framework 数据提供程序 | 用于 SQL Server 的 .NET Framework 数据访问接口 |
| Oracle |Microsoft OLE DB Provider for Oracle，适用于.NET 的 Oracle 数据提供程序 |用于.NET 的 oracle 数据提供程序 | |
| Teradata |OLE DB Provider for Teradata，适用于.NET 的 Teradata 数据提供程序 |用于.NET 的 Teradata 数据提供程序 | |
| | | |

> [!NOTE]
> 对于内存中模型，OLE DB 访问接口可以提供大规模的数据更好的性能。 在选择相同的数据源的不同访问接口时，请首先尝试 OLE DB 访问接口。  

### <a name="supported-by-in-memory-models-only"></a>支持的仅限内存中模型

|“数据库”  |
|---------|---------|---------|
|Access 数据库     | 
|SQL Server Analysis Services     | 
|IBM Informix （beta 版本） | 
|JSON 文档     | 
|从二进制文件的行     | 
|MySQL 数据库     | 
|PostgreSQL 数据库    | 是 | “否”
|SAP HANA   | 是 | “否”
|SAP Business Warehouse    | 是 | “否”
|Sybase 数据库     | 是 | “否”
|||

|文件  |  
|---------|---------|
|Excel 工作簿     |
|文件夹     | 
|JSON | 
|Text/CSV    | 
|XML 表    | 
|||

|联机服务  |  
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

[Azure Analysis Services 中支持的数据源](https://docs.microsoft.com/azure/analysis-services/analysis-services-datasource)   
