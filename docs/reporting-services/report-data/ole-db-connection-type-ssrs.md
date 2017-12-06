---
title: "OLE DB 连接类型 (SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-data
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d00cb13b-e1c2-4300-a195-3da1430a2df1
caps.latest.revision: "8"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: b992697f895d6131a69d157472d2277ca136e7ad
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/05/2017
---
# <a name="ole-db-connection-type-ssrs"></a>OLE DB 连接类型 (SSRS)
  若要包含来自 OLE DB 数据访问接口的数据，您必须具有一个基于 OLE DB 类型的报表数据源的数据集。 此内置数据源类型基于 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] OLE DB 数据处理扩展插件。  
  
 OLE DB 是一项数据访问技术，客户端通过该技术可以连接到各种数据访问接口。 在选择数据源类型 OLE DB 之后，您必须选择特定的数据访问接口。 是否支持参数和凭据之类的功能取决于您所选择的数据访问接口。  
  
 使用本主题中的信息来生成一个数据源。 有关分步说明，请参阅 [添加和验证数据连接（报表生成器和 SSRS）](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)。  
  
##  <a name="Connection"></a> 连接字符串  
 用于 OLE DB 数据处理扩展插件的连接字符串取决于您想要的数据访问接口。 典型的连接字符串包含数据访问接口支持的名称/值对。 例如，下面的连接字符串为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 和 AdventureWorks 数据库指定 OLE DB 访问接口。  
  
```  
Provider=SQLNCLI10.1;Data Source=server; Initial Catalog=AdventureWorks  
```  
  
 您使用的连接字符串取决于您所连接到的外部数据源。 若要设置特定于数据访问接口的连接字符串属性，请在 **“数据源属性”** 对话框的 **“常规”** 页中，单击 **“生成”** 按钮以打开 **“连接属性”** 对话框。 通过 **“数据链接属性”** 对话框设置扩展数据源属性。  
  
 有关连接字符串的示例，请参阅 [报表生成器中的数据连接、数据源和连接字符串](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34)。  
  
  
##  <a name="Credentials"></a> 凭据  
 执行以下操作时需要提供凭据：运行查询、本地预览报表以及从报表服务器预览报表。  
  
 报表发布后，您可能需要更改数据源的凭据，以使报表在报表服务器上运行时，用于检索数据的权限有效。  
  
 有关详细信息，请参阅[数据连接、数据源和连接字符串（报表生成器和 SSRS）](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)或[在报表生成器中指定凭据](http://msdn.microsoft.com/library/7412ce68-aece-41c0-8c37-76a0e54b6b53)。  
  
###### <a name="special-characters-in-a-password"></a>密码中的特殊字符  
 如果将 OLE DB 数据源配置为提示输入密码或在连接字符串中包含密码，并且用户输入了带有如标点符号之类特殊字符的密码，则某些基础数据源驱动程序无法验证这些特殊字符。 处理报表时，可能会出现“密码无效”这一消息来指示此问题。  
  
> [!NOTE]  
>  建议您不要在连接字符串中添加登录信息（如密码）。 报表生成器在 **“数据源”** 对话框中提供了一个用于输入凭据的单独选项卡。  
  
  
##  <a name="Parameters"></a> Parameters  
 某些 OLE DB 访问接口支持未命名参数，而不支持命名参数。 通过在查询中使用占位符按位置传递参数。 占位字符由数据访问接口所支持的语法确定。  
  
  
##  <a name="Remarks"></a> 注释  
 OLEDB 是一项用于为特定数据源生成数据访问接口的本机技术。 OLEDB 基于 COM（组件对象模型）接口。 OLEDB 这项技术晚于 ODBC、早于 ADO.NET 数据访问接口。 与任何其他 COM 组件一样，OLEDB 数据访问接口注册到操作系统。 OLEDB 数据访问接口可从 Microsoft 和第三方供应商那里获得。 Microsoft 还提供 MSDASQL，即架起与 ODBC 驱动程序的通信桥梁的 OLEDB 数据访问接口。 有关详细信息，请参阅 [ODBC 连接类型 (SSRS)](../../reporting-services/report-data/odbc-connection-type-ssrs.md)。  
  
 若要成功检索到想要的数据，则必须提供数据访问接口支持的查询语法。 参数支持因数据访问接口而异。 有关详细信息，请参阅针对所选数据访问接口的主题。 例如：  
  
-   [Analysis Services OLE DB 提供程序（Analysis Services - 多维数据）](http://msdn.microsoft.com/library/cdeecd50-1d91-4162-a4a2-01c7799b02a8)  
  
-   [使用 .NET Framework Data Provider for Oracle](http://go.microsoft.com/fwlink/?LinkId=112314)  
  
-   [SQL Server Native Client (OLE DB)](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
 有关特定 OLE DB 数据提供程序的详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [联机丛书](http://go.microsoft.com/fwlink/?linkid=121312)中 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 文档中的 [Reporting Services 支持的数据源 (SSRS)](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)。  
  
  
##  <a name="HowTo"></a> 操作指南主题  
 本节包含使用数据连接、数据源和数据集的分步说明。  
  
 [添加和验证数据连接（报表生成器和 SSRS）](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [创建共享数据集或嵌入数据集（报表生成器和 SSRS）](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [向数据集添加筛选器（报表生成器和 SSRS）](../../reporting-services/report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
  
##  <a name="Related"></a> 相关章节  
 文档中的这些章节提供有关报表数据的深入概念性信息，以及有关如何定义、自定义和使用与数据相关的报表部件的步骤信息。  
  
 [报表数据集 (SSRS)](../../reporting-services/report-data/report-datasets-ssrs.md)  
 提供访问报表数据的概述。  
  
 [报表生成器中的数据连接、数据源和连接字符串](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34)  
 提供有关数据连接和数据源的信息。  
  
 [报表的嵌入数据集和共享数据集（报表生成器和 SSRS）](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 提供有关嵌入数据集和共享数据集的信息。  
  
 [数据集字段集合（报表生成器和 SSRS）](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
 提供有关查询生成的数据集字段集合的信息。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [联机丛书](http://go.microsoft.com/fwlink/?linkid=121312)中 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 文档中的 [Reporting Services 支持的数据源 (SSRS) ](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)。  
 提供有关每个数据扩展插件的平台和版本支持的详细信息。  
  
  
## <a name="see-also"></a>另请参阅  
 [报表参数（报表生成器和报表设计器）](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [对数据进行筛选、分组和排序（报表生成器和 SSRS）](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [表达式（报表生成器和 SSRS）](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  
