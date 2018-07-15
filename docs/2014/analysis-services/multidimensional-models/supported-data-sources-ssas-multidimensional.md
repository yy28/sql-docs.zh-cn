---
title: 支持的数据源 (SSAS 多维) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Analysis Services, data sources
- data sources [Analysis Services], about data sources
- Analysis Services, data sources
- connections [Analysis Services]
- SSAS, data sources
ms.assetid: c97e0f8d-7ddd-4941-8b51-e7832f30fbbe
caps.latest.revision: 59
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7c4d8c3c37b63568da63d65e9548b50c44bcc455
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37301167"
---
# <a name="data-sources-supported-ssas-multidimensional"></a>数据源受支持 (SSAS 多维)
  本主题介绍可以在多维模型中使用的数据源的类型。  
  
##  <a name="bkmk_supported_ds"></a> 支持的数据源  
 可以从下表的数据源中检索数据。 在您安装 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]时，安装程序不安装对每种数据源列出的访问接口。 某些访问接口可能已随其他应用程序安装在您的计算机上；否则您需要下载并安装这些访问接口。  
  
> [!NOTE]  
>  还可以使用第三方访问接口（如 Oracle OLE DB 访问接口）并借助这些第三方提供的支持，连接到第三方数据库。  
  
|||||  
|-|-|-|-|  
|数据源|版本|文件类型|提供程序<sup>1</sup>|  
|Access 数据库|Microsoft Access 2007、2010、2013。|.accdb 或 .mdb|Microsoft Jet 4.0 OLE DB 访问接口|  
|SQL Server 关系数据库<sup>5</sup>|Microsoft SQL Server 2005、 2008、 2008 R2、 2012、 2014年[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] <sup>2</sup>，SQL Server 并行数据仓库 (PDW) <sup>3</sup>|（不适用）|OLE DB Provider for SQL Server<br /><br /> SQL Server Native Client OLE DB 访问接口<br /><br /> SQL Server Native 11.0 Client OLE DB 访问接口<br /><br /> 用于 SQL 客户端的 .NET Framework 数据访问接口|  
|Oracle 关系数据库|Oracle 9i、10g、11g。|（不适用）|Oracle OLE DB 访问接口<br /><br /> 用于 Oracle 客户端的 .NET Framework 数据访问接口<br /><br /> 用于 SQL Server 的 .NET Framework 数据访问接口<br /><br /> MSDAORA OLE DB 访问接口<sup>4</sup><br /><br /> OraOLEDB<br /><br /> MSDASQL|  
|Teradata 关系数据库|Teradata V2R6、V12|（不适用）|TDOLEDB OLE DB 访问接口<br /><br /> Teradata 的 .NET 数据访问接口|  
|Informix 关系数据库|V11.10|（不适用）|Informix OLE DB 访问接口|  
|IBM DB2 关系数据库|8.1|（不适用）|DB2OLEDB|  
|Sybase Adaptive Server Enterprise (ASE) 关系数据库|15.0.2|（不适用）|Sybase OLE DB 访问接口|  
|其他关系数据库|（不适用）|（不适用）|OLE DB 访问接口|  
  
 <sup>1</sup>多维解决方案不支持 ODBC 数据源。 尽管 Analysis Services 可自行处理连接，但 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 中用于生成解决方案的设计器不能连接到 ODBC 数据源，即使在使用 MSDASQL 驱动程序时也是如此。 如果您的业务需求包括 ODBC 数据源，请考虑改为生成表格解决方案。  
  
 <sup>2</sup>的详细信息，请参阅[!INCLUDE[ssSDS](../../includes/sssds-md.md)]，然后在[azure.microsoft.com](http://go.microsoft.com/fwlink/?LinkID=157856)。  
  
 <sup>3</sup>有关详细信息[!INCLUDE[ssSDS](../../includes/sssds-md.md)]PDW，请参阅[SQL Server Parallel Data Warehouse](http://go.microsoft.com/fwlink/?LinkId=150895)。  
  
 <sup>4</sup>在某些情况下，使用 MSDAORA OLE DB 提供程序可能导致连接错误，特别是对于 Oracle 的较新版本。 如果您遇到任何错误，我们建议您使用为 Oracle 列出的其他访问接口之一。  
  
 <sup>5</sup>某些功能需要在本地运行的 SQL Server 关系数据库。 特别是写回和 ROLAP 存储要求基础数据源为 SQL Server 关系数据库。  
  
## <a name="see-also"></a>请参阅  
 [支持的数据源&#40;SSAS 表格&#41;](../tabular-models/data-sources-supported-ssas-tabular.md)   
 [多维模型中的数据源](data-sources-in-multidimensional-models.md)   
 [多维模型中的数据源视图](data-source-views-in-multidimensional-models.md)  
  
  
