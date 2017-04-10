---
title: "支持的数据源（SSAS 表格） | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d6c2b1b3-91fc-4175-af25-509946dc7f24
caps.latest.revision: 28
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 28
---
# 支持的数据源（SSAS 表格）
  本主题介绍可用于表格模型的数据源的类型。  
  
##  <a name="bkmk_supported_ds"></a> 用于内存中模型的受支持的数据源  
 可以从下表的数据源中导入数据。 在您安装 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]时，安装程序不安装对每种数据源列出的访问接口。 某些访问接口可能已随其他应用程序安装在您的计算机上；否则您需要下载并安装这些访问接口。  
  
|||||  
|-|-|-|-|  
|数据源|版本|文件类型|访问接口|  
|Access 数据库|Microsoft Access 2010 及更高版本。|.accdb 或 .mdb|ACE 14 OLE DB 访问接口|  
|SQL Server 关系数据库|Microsoft SQL Server 2008 及更高版本、Microsoft SQL Server 数据仓库 2008 及更高版本、Microsoft Azure SQL 数据库、Microsoft 分析平台系统 (AP)<br /><br /> <br /><br /> 请注意，Analytics Platform System (APS) 旧称为 SQL Server 并行仓库一体机 (PDW)。 最初，从 Analysis Services 连接到 PDW 需要特殊的数据提供程序。 在 SQL Server 2012 中，此提供程序进行了替换。 对于 SQL Server 2012 及更高版本，需要使用 SQL Server Native Client 连接到 PDW/APS。 有关 APS 的详细信息，请访问网站 [Microsoft Analytics Platform System](http://www.microsoft.com/en-us/server-cloud/products/analytics-platform-system/resources.aspx)。|（不适用）|OLE DB Provider for SQL Server<br /><br /> SQL Server Native Client OLE DB 访问接口<br /><br /> SQL Server Native 10.0 Client OLE DB 提供程序<br /><br /> 用于 SQL 客户端的 .NET Framework 数据访问接口|  
|Oracle 关系数据库|Oracle 9i 及更高版本。|（不适用）|Oracle OLE DB 访问接口<br /><br /> 用于 Oracle 客户端的 .NET Framework 数据访问接口<br /><br /> 用于 SQL Server 的 .NET Framework 数据访问接口<br /><br /> OraOLEDB<br /><br /> MSDASQL|  
|Teradata 关系数据库|Teradata V2R6 及更高版本|（不适用）|TDOLEDB OLE DB 访问接口<br /><br /> Teradata 的 .NET 数据访问接口|  
|Informix 关系数据库||（不适用）|Informix OLE DB 访问接口|  
|IBM DB2 关系数据库|8.1|（不适用）|DB2OLEDB|  
|Sybase Adaptive Server Enterprise (ASE) 关系数据库|15.0.2|（不适用）|Sybase OLE DB 访问接口|  
|其他关系数据库|（不适用）|（不适用）|OLE DB 访问接口或 ODBC 驱动程序|  
|文本文件|（不适用）|.txt、.tab、.csv|用于 Microsoft Access 的 ACE 14 OLE DB 访问接口|  
|Microsoft Excel 文件|Excel 2010 及更高版本|.xlsx、xlsm、.xlsb、.xltx、.xltm|ACE 14 OLE DB 访问接口|  
|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿|Microsoft SQL Server 2008 及 Analysis Services 更高版本|xlsx、xlsm、.xlsb、.xltx、.xltm|ASOLEDB 10.5<br /><br /> （只能与发布到已安装 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 的 SharePoint 场的 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 工作簿一起使用）|  
|Analysis Services 多维数据集|Microsoft SQL Server 2008 及 Analysis Services 更高版本|（不适用）|ASOLEDB 10|  
|数据馈送<br /><br /> （用于从 Reporting Services 报表、Atom 服务文档、Microsoft Azure Marketplace DataMarket 和单个数据馈送导入数据）|Atom 1.0 格式<br /><br /> 作为 Windows Communication Foundation (WCF) Data Service（以前称作 ADO.NET Data Services）公开的任何数据库或文档。|服务文档的可定义一个或多个馈送的 .atomsvc<br /><br /> Atom Web 馈送文档的 .atom|Microsoft 数据馈送提供程序 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]<br /><br /> .NET Framework 数据馈送数据提供程序 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]|  
|Office 数据库连接文件||.odc||  
  
  
##  <a name="bkmk_supported_ds_dq"></a> 用于 DirectQuery 模型的受支持的数据源  
 DirectQuery 是内存中存储模式的一种替代模式，可将查询路由到后端数据系统并直接从中返回结果，而不是在模型内部（以及 RAM 中，如果模型已加载）存储所有数据。 由于 Analysis Services 必须使用本机数据库查询语法来表述查询，因此，对于这种模式，支持较小的数据源子集。  
  
数据源   |版本  |访问接口
---------|---------|---------
Microsoft SQL Server    |  2008 及更高版本      |       SQL Server 的 OLE DB 提供程序、SQL Server Native Client OLE DB 提供程序、SQL 客户端的 .NET Framework 数据提供程序  
Microsoft Azure SQL 数据库    |   全部      |  SQL Server 的 OLE DB 提供程序、SQL Server Native Client OLE DB 提供程序、SQL 客户端的 .NET Framework 数据提供程序            
Microsoft Azure SQL 数据仓库     |   全部     |  SQL Server Native Client OLE DB 提供程序、SQL 客户端的 .NET Framework 数据提供程序       
Microsoft SQL 分析平台系统 (APS)     |   全部      |  SQL Server 的 OLE DB 提供程序、SQL Server Native Client OLE DB 提供程序、SQL 客户端的 .NET Framework 数据提供程序       
Oracle 关系数据库     |  Oracle 9i 及更高版本       |  Oracle OLE DB 访问接口       
Teradata 关系数据库    |  Teradata V2R6 及更高版本     | Teradata 的 .NET 数据访问接口    

  
##  <a name="bkmk_tips"></a> 选择数据源的提示  
  
 从关系数据库导入表可以省去一些操作步骤，因为在导入过程中将使用外键关系在模型设计器的各表之间创建关系。  
  
导入多个表，然后删除不需要的表，这样也可以省去一些操作步骤。 如果一次导入一个表，则仍可能需要手动创建表之间的关系。  
  
不同数据源中包含类似数据的列是在模型设计器中创建关系的基础。 在使用异类数据源时，应选择包含这样的列的表：这些列可以映射到其他数据源中包含相同或类似数据的表。  
  
OLE DB 访问接口有时可为大型数据提供更快的性能。 在为同一数据源选择不同访问接口时，应首先尝试 OLE DB 访问接口。  
  
## 另请参阅  
 [数据源（SSAS 表格）](../../analysis-services/tabular-models/data-sources-ssas-tabular.md)   
 [导入数据（SSAS 表格）](../Topic/Import%20Data%20\(SSAS%20Tabular\).md)  
  
  