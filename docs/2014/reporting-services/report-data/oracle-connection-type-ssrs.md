---
title: Oracle 连接类型 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9db86dd2-beda-42d8-8af7-2629d58a8e3d
caps.latest.revision: 8
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: bab513aa3ad7349db0e45c9d3862aadf1499ca5f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36126013"
---
# <a name="oracle-connection-type-ssrs"></a>Oracle 连接类型 (SSRS)
  若要在报表中使用来自 Oracle 数据库的数据，您必须拥有一个基于 Oracle 类型的报表数据源的数据集。 此内置数据源类型基于 .NET Framework Managed Provider for Oracle，并且需要 Oracle 客户端软件组件。  
  
 使用本主题中的信息来生成一个数据源。 有关分步说明，请参阅[添加并验证数据连接或数据源&#40;报表生成器和 SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md)。  
  
##  <a name="Connection"></a> 连接字符串  
 请联系数据库管理员，获取连接信息以及用于连接到数据源的凭据。 下面的连接字符串示例指定使用 Unicode 的名为“Oracle9”的服务器上的 Oracle 数据库。 服务器名称必须与 Tnsnames.ora 配置文件中定义的 Oracle 服务器实例名相匹配。  
  
```  
Data Source="Oracle9"; Unicode="True"  
```  
  
 有关连接字符串示例的详细信息，请参阅 [报表生成器中的数据连接、数据源和连接字符串](../data-connections-data-sources-and-connection-strings-in-report-builder.md)。  
  
##  <a name="Credentials"></a> 凭据  
 执行以下操作时需要提供凭据：运行查询、本地预览报表以及从报表服务器预览报表。  
  
 报表发布后，您可能需要更改数据源的凭据，以使报表在报表服务器上运行时，用于检索数据的权限有效。  
  
 有关详细信息，请参阅[数据连接、 数据源和 Reporting Services 中的连接字符串](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)或[在报表生成器中指定凭据](../specify-credentials-in-report-builder.md)。  
  

  
##  <a name="Query"></a> 查询  
 若要创建数据集，可以从下拉列表中选择存储过程，也可以创建一个 SQL 查询。 若要生成一个查询，必须使用基于文本的查询设计器。 有关详细信息，请参阅[基于文本的查询设计器用户界面（报表生成器）](text-based-query-designer-user-interface-report-builder.md)。  
  
 可以指定只返回一个结果集的存储过程。 不支持使用基于游标的查询。  
  
##  <a name="Parameters"></a> Parameters  
 如果查询包括查询变量，则将自动生成对应的报表参数。 此扩展插件支持命名参数。 对于 Oracle 版本 9 或更高版本而言，支持多值参数。  
  
 报表参数是用可能需要修改的默认属性值创建的。 例如，每个报表参数的数据类型均为 **Text**。 创建报表参数后，您可能需要更改默认值。 有关详细信息，请参阅[报表参数（报表生成器和报表设计器）](../report-design/report-parameters-report-builder-and-report-designer.md)。  
  

  
##  <a name="Remarks"></a> 注释  
 在可以连接 Oracle 数据源之前，系统管理员必须已安装支持从 Oracle 数据库中检索数据的 .NET Data Provider for Oracle 版本。 此数据访问接口必须与报表生成器安装在同一台计算机上，报表服务器上也是如此。  
  
 有关详细信息，请参见以下内容：  
  
-   msdn.microsoft.com 上的[Using the .NET Framework Data Provider for Oracle](http://go.microsoft.com/fwlink/?LinkId=112314) （使用用于 Oracle 的 .NET Framework 数据访问接口）。  
  
-   [如何使用 Reporting Services 配置和访问 Oracle 数据源](http://support.microsoft.com/kb/834305)  
  
-   [如何为 NETWORK SERVICE 安全主体添加权限](http://support.microsoft.com/kb/870668)  
  
###### <a name="alternate-data-extensions"></a>备用数据扩展插件  
 您还可以通过使用 OLE DB 数据源类型从 Oracle 数据库中检索数据。 有关详细信息，请参阅 [OLE DB 连接类型 (SSRS)](ole-db-connection-type-ssrs.md)。  
  
###### <a name="report-models"></a>报表模型  
 您还可以创建基于 Oracle 数据库的模型。  
  
###### <a name="platform-and-version-information"></a>平台和版本信息  
 有关平台和版本支持的详细信息，请参阅 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][联机丛书](http://go.microsoft.com/fwlink/?linkid=121312)的 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 文档中的 [Reporting Services 支持的数据源 (SSRS)](../create-deploy-and-manage-mobile-and-paginated-reports.md)。  
  

  
##  <a name="HowTo"></a> 操作指南主题  
 本节包含使用数据连接、数据源和数据集的分步说明。  
  
 [添加并验证数据连接或数据源&#40;报表生成器和 SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [创建共享数据集或嵌入数据集（报表生成器和 SSRS）](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [向数据集添加筛选器（报表生成器和 SSRS）](add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
 
  
##  <a name="Related"></a> 相关章节  
 文档中的这些章节提供有关报表数据的深入概念性信息，以及有关如何定义、自定义和使用与数据相关的报表部件的步骤信息。  
  
 [向报表添加数据&#40;报表生成器和 SSRS&#41;](report-datasets-ssrs.md)  
 提供访问报表数据的概述。  
  
 [报表生成器中的数据连接、数据源和连接字符串](../data-connections-data-sources-and-connection-strings-in-report-builder.md)  
 提供有关数据连接和数据源的信息。  
  
 [报表的嵌入数据集和共享数据集（报表生成器和 SSRS）](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 提供有关嵌入数据集和共享数据集的信息。  
  
 [数据集字段集合（报表生成器和 SSRS）](dataset-fields-collection-report-builder-and-ssrs.md)  
 提供有关查询生成的数据集字段集合的信息。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [联机丛书](http://go.microsoft.com/fwlink/?linkid=121312)中 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 文档中的 [Reporting Services 支持的数据源 (SSRS) ](../create-deploy-and-manage-mobile-and-paginated-reports.md)。  
 提供有关每个数据扩展插件的平台和版本支持的详细信息。  
  

  
## <a name="see-also"></a>请参阅  
 [报表参数（报表生成器和报表设计器）](../report-design/report-parameters-report-builder-and-report-designer.md)   
 [对数据进行筛选、分组和排序（报表生成器和 SSRS）](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [表达式（报表生成器和 SSRS）](../report-design/expressions-report-builder-and-ssrs.md)  
  
  