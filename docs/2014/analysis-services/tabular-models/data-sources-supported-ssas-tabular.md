---
title: 支持的数据源（SSAS 表格） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: d6c2b1b3-91fc-4175-af25-509946dc7f24
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 345e733e5c1e90f637efab02a9942e307c2fb9f4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66067383"
---
# <a name="data-sources-supported-ssas-tabular"></a>支持的数据源（SSAS 表格）
  本主题介绍可用于表格模型的数据源的类型。  
  
 本文包含以下各节：  
  
-   [支持的数据源](#bkmk_supported_ds)  
  
-   [不支持的源](#bkmk_unsupported_ds)  
  
-   [选择数据源的提示](#bkmk_tips)  
  
##  <a name="supported-data-sources"></a><a name="bkmk_supported_ds"></a>支持的数据源  
 可以从下表的数据源中导入数据。 在您安装 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]时，安装程序不安装对每种数据源列出的访问接口。 某些访问接口可能已随其他应用程序安装在您的计算机上；否则您需要下载并安装这些访问接口。  
  
|||||  
|-|-|-|-|  
|源|版本|文件类型|提供程序<sup>1</sup>|  
|Access 数据库|Microsoft Access 2003、2007、2010。|.accdb 或 .mdb|ACE 14 OLE DB 访问接口|  
|SQL Server 关系数据库|Microsoft SQL Server2005，2008，2008 R2;SQL Server 2012，Microsoft SQL Azure 数据库<sup>2</sup>|（不适用）|OLE DB Provider for SQL Server<br /><br /> SQL Server Native Client OLE DB 访问接口<br /><br /> SQL Server Native 10.0 Client OLE DB 提供程序<br /><br /> 用于 SQL 客户端的 .NET Framework 数据访问接口|  
|SQL Server 并行数据仓库（PDW） <sup>3</sup>|2008 R2|（不适用）|OLE DB provider for SQL Server PDW|  
|Oracle 关系数据库|Oracle 9i、10g、11g。|（不适用）|Oracle OLE DB 访问接口<br /><br /> 用于 Oracle 客户端的 .NET Framework 数据访问接口<br /><br /> 用于 SQL Server 的 .NET Framework 数据访问接口<br /><br /> OraOLEDB<br /><br /> MSDASQL|  
|Teradata 关系数据库|Teradata V2R6、V12|（不适用）|TDOLEDB OLE DB 访问接口<br /><br /> Teradata 的 .NET 数据访问接口|  
|Informix 关系数据库||（不适用）|Informix OLE DB 访问接口|  
|IBM DB2 关系数据库|8.1|（不适用）|DB2OLEDB|  
|Sybase Adaptive Server Enterprise (ASE) 关系数据库|15.0.2|（不适用）|Sybase OLE DB 访问接口|  
|其他关系数据库|（不适用）|（不适用）|OLE DB 访问接口或 ODBC 驱动程序|  
|文本文件|（不适用）|.txt、.tab、.csv|用于 Microsoft Access 的 ACE 14 OLE DB 访问接口|  
|Microsoft Excel 文件|Excel 97-2003、2007、2010|.xlsx、xlsm、.xlsb、.xltx、.xltm|ACE 14 OLE DB 访问接口|  
|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 工作簿|Microsoft SQL Server 2008 R2 Analysis Services|xlsx、xlsm、.xlsb、.xltx、.xltm|ASOLEDB 10.5<br /><br /> （只能与发布到已安装 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 的 SharePoint 场的 [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 工作簿一起使用）|  
|Analysis Services 多维数据集|Microsoft SQL Server 2005、2008、2008 R2 Analysis Services|（不适用）|ASOLEDB 10|  
|数据馈送<br /><br /> （用于从 Reporting Services 报表、Atom 服务文档、Microsoft Azure 市场 DataMarket 和单个数据馈送导入数据）|Atom 1.0 格式<br /><br /> 作为 Windows Communication Foundation (WCF) Data Service（以前称作 ADO.NET Data Services）公开的任何数据库或文档。|服务文档的可定义一个或多个馈送的 .atomsvc<br /><br /> Atom Web 馈送文档的 .atom|Microsoft 数据馈送提供程序 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]<br /><br /> .NET Framework 数据馈送数据提供程序 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]|  
|Office 数据库连接文件||.odc||  
  
 <sup>1</sup>还可以使用用于 ODBC 的 OLE DB 提供程序。  
  
 <sup>2</sup>有关 SQL Azure 的详细信息，请参阅网站[SQL Azure](https://go.microsoft.com/fwlink/?LinkID=157856)。  
  
 <sup>3</sup>有关 SQL Server PDW 的详细信息，请参阅网站[SQL Server 2008 R2 并行数据仓库](https://go.microsoft.com/fwlink/?LinkId=150895)。  
  
 <sup>4</sup>在某些情况下，使用 MSDAORA OLE DB 提供程序可能会导致连接错误，特别是在较新版本的 Oracle 上。 如果您遇到任何错误，我们建议您使用为 Oracle 列出的其他访问接口之一。  
  
##  <a name="unsupported-sources"></a><a name="bkmk_unsupported_ds"></a>不支持的源  
 目前不支持以下数据源：  
  
-   无法导入服务器文档，例如，已发布到 SharePoint 的 Access 数据库。  
  
##  <a name="tips-for-choosing-data-sources"></a><a name="bkmk_tips"></a>选择数据源的提示  
  
1.  ** 从关系数据库导入表可以省去一些操作步骤，因为在导入过程中将使用外键关系在模型设计器的各表之间创建关系。  
  
2.  导入多个表，然后删除不需要的表，这样也可以省去一些操作步骤。 如果一次导入一个表，则仍可能需要手动创建表之间的关系。  
  
3.  不同数据源中包含类似数据的列是在模型设计器中创建关系的基础。 在使用异类数据源时，应选择包含这样的列的表：这些列可以映射到其他数据源中包含相同或类似数据的表。  
  
4.  {0}OLE DB 访问接口有时可为大型数据提供更快的性能。{0} 在为同一数据源选择不同访问接口时，应首先尝试 OLE DB 访问接口。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;SSAS 表格&#41;的数据源](../data-sources-ssas-tabular.md)   
 [导入数据（SSAS 表格）](../import-data-ssas-tabular.md)  
  
  
