---
title: Teradata 连接类型 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: b02779c2-a6b9-453c-815f-adad53353952
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 4ce9fb555cce7913939eb8e611a319d7a938c064
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56016508"
---
# <a name="teradata-connection-type-ssrs"></a>Teradata 连接类型 (SSRS)
  若要在报表中包含来自 Teradata 关系数据库的数据，您必须拥有一个基于 Teradata 类型的报表数据源的数据集。 此内置数据源类型基于 .NET Managed Provider for Teradata 数据处理扩展插件。  
  
 使用本主题中的信息来生成一个数据源。 有关分步说明，请参阅[添加和验证数据连接或数据源&#40;报表生成器和 SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md)。  
  
##  <a name="Connection"></a> 连接字符串  
 请联系数据库管理员，获取连接信息以及用于连接到数据源的凭据。 下面的连接字符串示例指定使用 IP 地址指定的服务器上的 Teradata 数据库：  
  
```  
data source=<IP Address>  
```  
  
 有关更多连接字符串的示例，请参阅 [报表生成器中的数据连接、数据源和连接字符串](../data-connections-data-sources-and-connection-strings-in-report-builder.md)。  
  
##  <a name="Credentials"></a> 凭据  
 执行以下操作时需要提供凭据：运行查询、本地预览报表以及从报表服务器预览报表。  
  
 报表发布后，您可能需要更改数据源的凭据，以使报表在报表服务器上运行时，用于检索数据的权限有效。  
  
 有关详细信息，请参阅[数据连接、 数据源和 Reporting Services 中的连接字符串](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)或[在报表生成器中指定凭据](../specify-credentials-in-report-builder.md)。  
  
 ![用于“返回页首”链接的箭头图标](../../2014-toc/media/uparrow16x16.gif "用于“返回页首”链接的箭头图标")[返回页首](#BackToTop)  
  
##  <a name="Remarks"></a> 注释  
 在可以连接 Teradata 数据源之前，系统管理员必须已安装支持从 Teradata 数据库中检索数据的 .NET Data Provider for Teradata 版本。 此数据访问接口必须与报表生成器安装在同一台计算机上，报表服务器上也是如此。  
  
 不是所有的报表传递模式都受到此数据访问接口的支持。 此数据处理扩展插件不支持通过数据驱动订阅传递报表。 有关详细信息，请参阅 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [ 联机丛书 ](https://go.microsoft.com/fwlink/?linkid=121312) 中 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 文档中的[使用外部数据源提供订阅方数据（数据驱动订阅）](../subscriptions/use-an-external-data-source-for-subscriber-data-data-driven-subscription.md)。  
  
 ![用于“返回页首”链接的箭头图标](../../2014-toc/media/uparrow16x16.gif "用于“返回页首”链接的箭头图标")[返回页首](#BackToTop)  
  
##  <a name="Models"></a> 报表模型  
 若要从基于 Teradata 数据源的报表模型创建数据集，则模型必须在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中的模型设计器内设计，并在报表服务器上发布。  
  
 ![用于“返回页首”链接的箭头图标](../../2014-toc/media/uparrow16x16.gif "用于“返回页首”链接的箭头图标")[返回页首](#BackToTop)  
  
##  <a name="Related"></a> 相关章节  
 文档中的这些章节提供有关报表数据的深入概念性信息，以及有关如何定义、自定义和使用与数据相关的报表部件的步骤信息。  
  
 [向报表添加数据&#40;报表生成器和 SSRS&#41;](report-datasets-ssrs.md)  
 提供访问报表数据的概述。  
  
 [报表生成器中的数据连接、数据源和连接字符串](../data-connections-data-sources-and-connection-strings-in-report-builder.md)  
 提供有关数据连接和数据源的信息。  
  
 [报表的嵌入数据集和共享数据集（报表生成器和 SSRS）](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 提供有关嵌入数据集和共享数据集的信息。  
  
 [数据集字段集合（报表生成器和 SSRS）](dataset-fields-collection-report-builder-and-ssrs.md)  
 提供有关数据集查询生成的字段集合的信息。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [联机丛书](https://go.microsoft.com/fwlink/?linkid=121312)中 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 文档中的 [Reporting Services 支持的数据源 (SSRS) ](../create-deploy-and-manage-mobile-and-paginated-reports.md)。  
 提供有关每个数据扩展插件的平台和版本支持的详细信息。  
  
 [将 SQL Server 2008 Reporting Services 与 .NET Framework Data Provider for Teradata 一起使用](https://go.microsoft.com/fwlink/?LinkID=130848)  
 提供有关使用此数据扩展插件的详细信息。  
  
 ![用于“返回页首”链接的箭头图标](../../2014-toc/media/uparrow16x16.gif "用于“返回页首”链接的箭头图标")[返回页首](#BackToTop)  
  
## <a name="see-also"></a>请参阅  
 [报表参数（报表生成器和报表设计器）](../report-design/report-parameters-report-builder-and-report-designer.md)   
 [对数据进行筛选、分组和排序（报表生成器和 SSRS）](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [表达式（报表生成器和 SSRS）](../report-design/expressions-report-builder-and-ssrs.md)  
  
  
