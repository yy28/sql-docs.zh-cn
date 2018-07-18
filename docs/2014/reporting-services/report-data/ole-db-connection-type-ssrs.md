---
title: OLE DB 连接类型 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: d00cb13b-e1c2-4300-a195-3da1430a2df1
caps.latest.revision: 8
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: bf944dfa9bd17946130b568d53be032c56fc0ef3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37198747"
---
# <a name="ole-db-connection-type-ssrs"></a>OLE DB 连接类型 (SSRS)
  若要包含来自 OLE DB 数据访问接口的数据，您必须具有一个基于 OLE DB 类型的报表数据源的数据集。 此内置数据源类型基于 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] OLE DB 数据处理扩展插件。  
  
 OLE DB 是一项数据访问技术，客户端通过该技术可以连接到各种数据访问接口。 在选择数据源类型 OLE DB 之后，您必须选择特定的数据访问接口。 是否支持参数和凭据之类的功能取决于您所选择的数据访问接口。  
  
 使用本主题中的信息来生成一个数据源。 有关分步说明，请参阅[添加和验证数据连接或数据源&#40;报表生成器和 SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md)。  
  
##  <a name="Connection"></a> 连接字符串  
 用于 OLE DB 数据处理扩展插件的连接字符串取决于您想要的数据访问接口。 典型的连接字符串包含数据访问接口支持的名称/值对。 例如，下面的连接字符串为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 和 AdventureWorks 数据库指定 OLE DB 访问接口。  
  
```  
Provider=SQLNCLI10.1;Data Source=server; Initial Catalog=AdventureWorks  
```  
  
 您使用的连接字符串取决于您所连接到的外部数据源。 若要设置特定于数据访问接口的连接字符串属性，请在 **“数据源属性”** 对话框的 **“常规”** 页中，单击 **“生成”** 按钮以打开 **“连接属性”** 对话框。 通过 **“数据链接属性”** 对话框设置扩展数据源属性。  
  
 有关连接字符串的示例，请参阅 [报表生成器中的数据连接、数据源和连接字符串](../data-connections-data-sources-and-connection-strings-in-report-builder.md)。  
  
  
  
##  <a name="Credentials"></a> 凭据  
 执行以下操作时需要提供凭据：运行查询、本地预览报表以及从报表服务器预览报表。  
  
 报表发布后，您可能需要更改数据源的凭据，以使报表在报表服务器上运行时，用于检索数据的权限有效。  
  
 有关详细信息，请参阅[数据连接、 数据源和 Reporting Services 中的连接字符串](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)或[在报表生成器中指定凭据](../specify-credentials-in-report-builder.md)。  
  
###### <a name="special-characters-in-a-password"></a>密码中的特殊字符  
 如果将 OLE DB 数据源配置为提示输入密码或在连接字符串中包含密码，并且用户输入了带有如标点符号之类特殊字符的密码，则某些基础数据源驱动程序无法验证这些特殊字符。 处理报表时，可能会出现“密码无效”这一消息来指示此问题。  
  
> [!NOTE]  
>  建议您不要在连接字符串中添加登录信息（如密码）。 报表生成器在 **“数据源”** 对话框中提供了一个用于输入凭据的单独选项卡。  
  
  
  
##  <a name="Parameters"></a> Parameters  
 某些 OLE DB 访问接口支持未命名参数，而不支持命名参数。 通过在查询中使用占位符按位置传递参数。 占位字符由数据访问接口所支持的语法确定。  
  
 
  
##  <a name="Remarks"></a> 注释  
 OLEDB 是一项用于为特定数据源生成数据访问接口的本机技术。 OLEDB 基于 COM（组件对象模型）接口。 OLEDB 这项技术晚于 ODBC、早于 ADO.NET 数据访问接口。 与任何其他 COM 组件一样，OLEDB 数据访问接口注册到操作系统。 OLEDB 数据访问接口可从 Microsoft 和第三方供应商那里获得。 Microsoft 还提供 MSDASQL，即架起与 ODBC 驱动程序的通信桥梁的 OLEDB 数据访问接口。 有关详细信息，请参阅 [ODBC 连接类型 (SSRS)](odbc-connection-type-ssrs.md)。  
  
 若要成功检索到想要的数据，则必须提供数据访问接口支持的查询语法。 参数支持因数据访问接口而异。 有关详细信息，请参阅针对所选数据访问接口的主题。 例如：  
  
-   [Analysis Services OLE DB 提供程序&#40;Analysis Services-多维数据&#41;](../../analysis-services/dev-guide/analysis-services-ole-db-provider-analysis-services-multidimensional-data.md)  
  
-   [使用 .NET Framework Data Provider for Oracle](http://go.microsoft.com/fwlink/?LinkId=112314)  
  
-   [SQL Server Native Client (OLE DB)](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
 有关特定 OLE DB 数据提供程序的详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [联机丛书](http://go.microsoft.com/fwlink/?linkid=121312)中 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 文档中的 [Reporting Services 支持的数据源 (SSRS)](../create-deploy-and-manage-mobile-and-paginated-reports.md)。  
  
  
  
##  <a name="HowTo"></a> 操作指南主题  
 本节包含使用数据连接、数据源和数据集的分步说明。  
  
 [添加和验证数据连接或数据源&#40;报表生成器和 SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
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
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [联机丛书](http://go.microsoft.com/fwlink/?linkid=121312)中 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 文档中的 [Reporting Services 支持的数据源 (SSRS) ](../create-deploy-and-manage-mobile-and-paginated-reports.md)。  
 提供有关每个数据扩展插件的平台和版本支持的详细信息。  
  
 
  
## <a name="see-also"></a>请参阅  
 [报表参数（报表生成器和报表设计器）](../report-design/report-parameters-report-builder-and-report-designer.md)   
 [对数据进行筛选、分组和排序（报表生成器和 SSRS）](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [表达式（报表生成器和 SSRS）](../report-design/expressions-report-builder-and-ssrs.md)  
  
  
