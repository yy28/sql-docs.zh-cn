---
title: 在 SQL Server Analysis Services 表格 1200年模型中支持的数据源 |Microsoft Docs
ms.date: 07/02/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a1ef7ae48e3d1500d08c9adba5e39db6214125c5
ms.sourcegitcommit: d9c5b9ab3c282775ed61712892eeb3e150ccc808
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/05/2019
ms.locfileid: "67597360"
---
# <a name="data-sources-supported-in-sql-server-analysis-services-tabular-1200-models"></a>数据源支持在 SQL Server Analysis Services 中表格 1200年模型
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  
本文介绍可以用于 SQL Server Analysis Services 表格 1200年模型和低的兼容级别的数据源的类型。 

在 1400年兼容性级别的模型，请参阅[支持在 SQL Server Analysis Services 表格 1400年模型中的数据源](data-sources-supported-ssas-tabular-1400.md)。

Azure Analysis Services，请参阅[支持 Azure Analysis Services 中的数据源](https://docs.microsoft.com/azure/analysis-services/analysis-services-datasource)。
  
##  <a name="bkmk_supported_ds"></a> 内存中表格模型的支持的数据源  
在您安装 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]时，安装程序不安装对每种数据源列出的访问接口。 某些提供程序可能与您的计算机上的其他应用程序安装。 在其他情况下，可能需要下载并安装提供程序。  
  
|||||  
|-|-|-|-|  
|Source|版本|文件类型|访问接口|  
|Access 数据库|Microsoft Access 2010 及更高版本。|.accdb 或 .mdb|ACE 14 OLE DB 访问接口<sup> [1](#dnu)</sup>|  
|SQL Server 关系数据库|SQL Server 2008 和更高版本、 SQL Server 数据仓库 2008年和更高版本、 Azure SQL 数据库，Azure SQL 数据仓库、 Analytics Platform System (APS)<br /><br /> <br /><br /> Analytics Platform System (APS) 旧称为 SQL Server 并行数据仓库 (PDW)。 最初，从 Analysis Services 连接到 PDW 需要特殊的数据提供程序。 在 SQL Server 2012 中，此提供程序进行了替换。 对于 SQL Server 2012 及更高版本，需要使用 SQL Server Native Client 连接到 PDW/APS。 |（不适用）|OLE DB Provider for SQL Server<br /><br /> SQL Server Native Client OLE DB 访问接口<br /><br /> SQL Server Native 10.0 Client OLE DB 提供程序<br /><br /> 用于 SQL 客户端的 .NET Framework 数据访问接口|  
|Oracle 关系数据库|Oracle 9i 及更高版本。|（不适用）|Oracle OLE DB 访问接口<br /><br /> 用于 Oracle 客户端的 .NET Framework 数据访问接口<br /><br /> 用于 SQL Server 的 .NET Framework 数据访问接口<br /><br /> OraOLEDB<br /><br /> MSDASQL|  
|Teradata 关系数据库|Teradata V2R6 及更高版本|（不适用）|TDOLEDB OLE DB 访问接口<br /><br /> Teradata 的 .NET 数据访问接口|  
|Informix 关系数据库||（不适用）|Informix OLE DB 访问接口|  
|IBM DB2 关系数据库|8.1|（不适用）|DB2OLEDB|  
|Sybase Adaptive Server Enterprise (ASE) 关系数据库|15.0.2|（不适用）|Sybase OLE DB 访问接口|  
|其他关系数据库|（不适用）|（不适用）|OLE DB 访问接口或 ODBC 驱动程序|  
|文本文件|（不适用）|.txt、.tab、.csv|ACE 14 OLE DB 访问接口<sup> [1](#dnu)</sup> |  
|Microsoft Excel 文件|Excel 2010 及更高版本|.xlsx、xlsm、.xlsb、.xltx、.xltm|ACE 14 OLE DB 访问接口<sup> [1](#dnu)</sup>|  
|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿|Microsoft SQL Server 2008 及 Analysis Services 更高版本|xlsx、xlsm、.xlsb、.xltx、.xltm|ASOLEDB 10.5<br /><br /> （只能与发布到已安装 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 的 SharePoint 场的 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 工作簿一起使用）|  
|Analysis Services 多维数据集|Microsoft SQL Server 2008 及 Analysis Services 更高版本|（不适用）|ASOLEDB 10|  
|数据馈送<br /><br /> （用于从 Reporting Services 报表、Atom 服务文档、Microsoft Azure 市场 DataMarket 和单个数据馈送导入数据）|Atom 1.0 格式<br /><br /> 作为 Windows Communication Foundation (WCF) Data Service（以前称作 ADO.NET Data Services）公开的任何数据库或文档。|`.atomsvc` 它定义一个或多个馈送的服务文档<br /><br /> Atom Web 馈送文档的 .atom|Microsoft 数据馈送提供程序 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]<br /><br /> .NET Framework 数据馈送数据提供程序 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]|  
|Office 数据库连接文件||.odc||  
 
<a name="dnu">[1]</a> Using **ACE 14 OLE DB 访问接口**若要连接到文件数据类型**建议不要**。 如果必须保留在表格 1200年及更低版本兼容性级别模型，将数据导出到 csv 文件类型、 导入到 SQL 数据库，然后连接到和从数据库导入。 但是，建议您升级到表格 1400年兼容级别 (SQL Server 2017 及更高版本) 并使用**获取数据**SSDT，以选择并导入文件数据源中。 获取数据使用结构化的数据源连接提供的 Power Query 数据引擎，这是比 ACE 14 OLE DB 提供程序连接更稳定。  


##  <a name="bkmk_supported_ds_dq"></a> 用于 DirectQuery 模型的受支持的数据源  
 DirectQuery 是内存中存储模式的一种替代模式，可将查询路由到后端数据系统并直接从中返回结果，而不是在模型内部（以及 RAM 中，如果模型已加载）存储所有数据。 由于 Analysis Services 来表述查询的本机数据库查询语法，此模式下支持的数据源的较小子集。  
  
数据源   |版本  |访问接口
---------|---------|---------
Microsoft SQL Server    |  2008 及更高版本      |       SQL Server 的 OLE DB 提供程序、SQL Server Native Client OLE DB 提供程序、SQL 客户端的 .NET Framework 数据提供程序  
Microsoft Azure SQL 数据库    |   All      |  SQL Server 的 OLE DB 提供程序、SQL Server Native Client OLE DB 提供程序、SQL 客户端的 .NET Framework 数据提供程序            
Microsoft Azure SQL 数据仓库     |   All     |  SQL Server Native Client OLE DB 提供程序、SQL 客户端的 .NET Framework 数据提供程序       
Microsoft SQL 分析平台系统 (APS)     |   All      |  SQL Server 的 OLE DB 提供程序、SQL Server Native Client OLE DB 提供程序、SQL 客户端的 .NET Framework 数据提供程序       
|Microsoft SQL Server Always Encrypted <sup> [2](#ae)</sup> | 2016 及更高版本。 2014 及更早版本仅限于 Enterprise edition。 | 用于 SQL 客户端的 .NET Framework 数据访问接口
|始终加密的 azure SQL 数据库<sup> [2](#ae)</sup>| All | 用于 SQL 客户端的 .NET Framework 数据访问接口
Oracle 关系数据库     |  Oracle 9i 及更高版本       |  Oracle OLE DB 访问接口       
Teradata 关系数据库    |  Teradata V2R6 及更高版本     | Teradata 的 .NET 数据访问接口    


### <a name="using-sql-server-analysis-services-with-always-encrypted"></a>使用 SQL Server Analysis Services 与始终加密

<a name="ae">[2]</a> SQL Server Analysis Services 可以作为数据库使用的客户端[Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md)中 SQL Server 或 Azure SQL 数据库在以下情况下： 

*  保护已加密的列的列主密钥必须存储在 Windows 证书存储区中的证书。 不支持列主密钥的密钥存储在 Azure 密钥保管库中。   
*  在其安装 Analysis Services 的 Windows 计算机已安装必要的列主密匙证书。 若要了解详细信息，请参阅[在 Windows 证书存储区中创建列主密钥的密钥](../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md#creating-column-master-keys-in-windows-certificate-store)。
*  Analysis Services 用于连接到 SQL 数据源基于.Net Framework 提供程序，并且必须启用数据源上的属性的列加密设置。 .NET framework 4.6.1 或更高版本必须是 Analysis Services 服务器上存在。
*  SQL Server 或 SQL 数据库数据源必须是*提供程序*支持 1200年兼容级别的数据源类型。 它不会使用 Power Query*结构化*在 1400年兼容性级别中引入的数据源。
  
##  <a name="bkmk_tips"></a> 选择数据源的提示  
  
 从关系数据库导入表可以省去一些操作步骤，因为在导入过程中将使用外键关系在模型设计器的各表之间创建关系。  
  
导入多个表，然后删除不需要的表，这样也可以省去一些操作步骤。 如果一次导入一个表，则仍可能需要手动创建表之间的关系。  
  
不同数据源中包含类似数据的列是在模型设计器中创建关系的基础。 在使用异类数据源时，应选择包含这样的列的表：这些列可以映射到其他数据源中包含相同或类似数据的表。  
  
OLE DB 访问接口有时可以提供更快的大型数据的性能。 在为同一数据源选择不同访问接口时，应首先尝试 OLE DB 访问接口。  

## <a name="see-also"></a>另请参阅

[数据源支持在 SQL Server Analysis Services 中表格 1400年模型](data-sources-supported-ssas-tabular-1400.md)

[Azure Analysis Services 中支持的数据源](https://docs.microsoft.com/azure/analysis-services/analysis-services-datasource)   
