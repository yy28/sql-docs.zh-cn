---
title: Reporting Services 查询设计器 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- query designers [Reporting Services]
ms.assetid: 07efd3f1-804f-45f7-b62a-3e727a3d9835
caps.latest.revision: 16
author: maggiesmsft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: aed7304b4e7e48eff1691970da5ff68b03fd0962
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37222937"
---
# <a name="reporting-services-query-designers"></a>Reporting Services 查询设计器
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 提供了图形和基于文本的查询设计器，以帮助您生成查询的报表中每个数据源类型。  
  
 某些数据源支持以交互方式生成查询的图形设计器。 其他数据源使用基于文本的查询设计器。 使用图形查询设计器，可以将表示数据源中基础数据的元数据项拖到查询设计图面上。 使用基于文本的查询设计器，可以在查询窗格中键入命令文本。 单击工具栏上的基于文本的查询设计器图标，即可从图形查询设计器更改为基于文本的查询设计器。  
  
 在您的报表中可用的数据源类型由在您的客户端或报表服务器上安装的 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 数据扩展插件决定。 有关详细信息，请参阅[RSReportDesigner Configuration File](report-server/rsreportdesigner-configuration-file.md)并[RSReportServer 配置文件](report-server/rsreportserver-config-configuration-file.md)。  
  
 数据处理扩展插件及其关联的查询设计器在对数据源的支持上在以下方式上可能会不同：  
  
-   **查询设计器类型。** 例如， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据源同时支持图形查询设计器和基于文本的查询设计器。  
  
-   **查询语言变化。** 例如，像 [!INCLUDE[tsql](../includes/tsql-md.md)] 这样的查询语言在语法上可能有所不同，具体情况取决于数据源类型。 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[tsql](../includes/tsql-md.md)] 语言与 Oracle SQL 语言在查询命令的语法上有不同之处。  
  
-   **对数据库对象名的架构部分的支持。** 当数据源使用架构作为数据库对象标识符的一部分时，对于不使用默认架构的任何名称而言，必须将架构名作为查询的一部分提供。 例如， `SELECT FirstName, LastName FROM [Person].[Person]`。  
  
-   **对查询参数的支持。** 数据访问接口在为参数提供支持方面存在差异。 某些数据访问接口支持命名参数；例如， `SELECT Col1, Col2 FROM Table WHERE <parameter identifier><parameter name> = <value>`。 某些数据访问接口支持未命名参数；例如， `SELECT Col1, Col2 FROM Table WHERE <column name> = ?`。 参数标识符可能因数据提供程序;例如，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]使用"at"(@) 符号，而 Oracle 则使用冒号 （:）。 某些数据访问接口不支持参数。  
  
-   **能否导入查询。** 例如，对于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据源，可从报表定义文件 (.rdl) 或 .sql 文件中导入现有查询。  
  
## <a name="query-designers"></a>查询设计器  
 下面的主题将介绍每种查询设计器的用户界面。  
  
-   [Analysis Services MDX 查询设计器用户界面](report-data/analysis-services-mdx-query-designer-user-interface.md)  
  
-   [Analysis Services DMX 查询设计器用户界面](report-data/analysis-services-dmx-query-designer-user-interface.md)  
  
-   [图形查询设计器用户界面](report-data/graphical-query-designer-user-interface.md)  
  
-   [关系查询设计器用户界面](../../2014/reporting-services/relational-query-designer-user-interface.md)  
  
-   [Hyperion Essbase 查询设计器用户界面](report-data/hyperion-essbase-query-designer-user-interface.md)  
  
-   [报表模型查询设计器用户界面](report-data/report-model-query-designer-user-interface.md)  
  
-   [SAP NetWeaver BI 查询设计器用户界面](report-data/sap-netweaver-bi-query-designer-user-interface.md)  
  
-   [SharePoint 列表查询设计器](../../2014/reporting-services/sharepoint-list-query-designer.md)  
  
-   [基于文本的查询设计器用户界面](../../2014/reporting-services/text-based-query-designer-user-interface.md)  
  
## <a name="see-also"></a>请参阅  
 [Reporting Services 支持的数据源&#40;SSRS&#41;](create-deploy-and-manage-mobile-and-paginated-reports.md)   
 [从外部数据源中添加数据 (SSRS)](report-data/add-data-from-external-data-sources-ssrs.md)   
 [数据处理扩展插件和.NET Framework 数据提供程序&#40;SSRS&#41;](report-data/data-processing-extensions-and-net-framework-data-providers-ssrs.md)   
 [扩展&#40;SSRS&#41;](extensions-ssrs.md)  
  
  
