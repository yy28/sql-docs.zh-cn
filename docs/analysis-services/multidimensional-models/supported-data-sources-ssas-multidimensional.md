---
title: 支持的数据源 (SSAS-多维) |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 907e6cc6deaa9617a4af93ab2080bfe495dacd0b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208462"
---
# <a name="supported-data-sources-ssas---multidimensional"></a>支持的数据源（SSAS - 多维）
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  本主题介绍可以在多维模型中使用的数据源的类型。  
  
##  <a name="bkmk_supported_ds"></a> 支持的数据源  
 可以从下表的数据源中检索数据。 在您安装 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]时，安装程序不安装对每种数据源列出的访问接口。 某些访问接口可能已随其他应用程序安装在您的计算机上；否则您需要下载并安装这些访问接口。  
  
> [!NOTE]  
>  还可以使用第三方访问接口（如 Oracle OLE DB 访问接口）并借助这些第三方提供的支持，连接到第三方数据库。  
  
|||||  
|-|-|-|-|  
|Source|版本|文件类型|提供程序*|  
|Access 数据库|Microsoft Access 2010、2013、2016|.accdb 或 .mdb|Microsoft Jet 4.0 OLE DB 访问接口|  
|SQL Server 关系数据库*|Microsoft SQL Server 2008、 2008 R2、 2012年、 2014年、 2016年[!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]，Azure SQL 数据仓库、 Microsoft Analytics Platform System (APS)<br /><br /> <br /><br /> 注意:有关详细信息[!INCLUDE[ssSDS](../../includes/sssds-md.md)]上[Azure.com](http://go.microsoft.com/fwlink/?LinkID=157856)。<br /><br /> 注意:Analytics Platform System (APS) 旧称为 SQL Server 并行数据仓库 (PDW)。 最初，从 Analysis Services 连接到 PDW 需要特殊的数据提供程序。 在 SQL Server 2012 中，此提供程序进行了替换。 对于 SQL Server 2012 及更高版本，需要使用 SQL Server Native Client 连接到 PDW/APS。 有关 APS 的详细信息，请访问网站 [Microsoft Analytics Platform System](http://www.microsoft.com/en-us/server-cloud/products/analytics-platform-system/resources.aspx)。|（不适用）|OLE DB Provider for SQL Server<br /><br /> SQL Server Native Client OLE DB 访问接口<br /><br /> SQL Server Native 11.0 Client OLE DB 访问接口<br /><br /> 用于 SQL 客户端的 .NET Framework 数据访问接口|  
|Oracle 关系数据库|Oracle 9i、10g、11g、12g|（不适用）|Oracle OLE DB 访问接口<br /><br /> 用于 Oracle 客户端的 .NET Framework 数据访问接口<br /><br /> 用于 SQL Server 的 .NET Framework 数据访问接口<br /><br /> OraOLEDB<br /><br /> MSDASQL|  
|Teradata 关系数据库|Teradata V2R6、V12|（不适用）|TDOLEDB OLE DB 访问接口<br /><br /> Teradata 的 .NET 数据访问接口|  
|Informix 关系数据库|V11.10|（不适用）|Informix OLE DB 访问接口|  
|IBM DB2 关系数据库|8.1|（不适用）|DB2OLEDB|  
|Sybase Adaptive Server Enterprise (ASE) 关系数据库|15.0.2|（不适用）|Sybase OLE DB 访问接口|  
|其他关系数据库|（不适用）|（不适用）|OLE DB 访问接口|  
  
 \* 多维解决方案不支持 ODBC 数据源。 尽管 Analysis Services 可自行处理连接，但 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 中用于生成解决方案的设计器不能连接到 ODBC 数据源，即使在使用 MSDASQL 驱动程序时也是如此。 如果你的业务需求包括 ODBC 数据源，请考虑改为生成表格解决方案。  
  
 **某些功能要求安装可在本地运行的 SQL Server 关系数据库才能正常运行。 特别是写回和 ROLAP 存储，它们要求基础数据源必须是 SQL Server 关系数据库。  
  
## <a name="see-also"></a>请参阅  
 [支持的数据源](../../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md)   
 [多维模型中的数据源](../../analysis-services/multidimensional-models/data-sources-in-multidimensional-models.md)   
 [多维模型中的数据源视图](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)  
  
  
