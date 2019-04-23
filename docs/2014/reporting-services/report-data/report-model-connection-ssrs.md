---
title: 报表模型连接 (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: da880fb8-13cc-4d5f-b992-91ed0ec3ca7d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b93ba187e20f4e8c0c8d9574383f91cfd887a9ac
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59944183"
---
# <a name="report-model-connection-ssrs"></a>报表模型连接 (SSRS)
  若要包含来自报表模型的数据，必须拥有一个基于作为数据源的报表模型的数据集。 与其他报表数据源不同，报表模型没有数据扩展插件。 在报表生成器中，您可以浏览到该模型或者从报表服务器直接选择该模型。 在报表设计器中，您指定指向报表模型的 URL。  
  
 使用本主题中的信息来生成一个数据源。 有关分步说明，请参阅[添加和验证数据连接或数据源&#40;报表生成器和 SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md)。  
  
##  <a name="Connection"></a> 连接字符串  
 无需连接字符串即可将报表模型用作数据源。 若要连接到报表模型，请浏览到报表服务器或 SharePoint 站点并选择已发布的模型。 在 SharePoint 站点上，报表模型文件扩展名为 .smdl。  
  
 有关更多连接字符串的示例，请参阅 [报表生成器中的数据连接、数据源和连接字符串](../data-connections-data-sources-and-connection-strings-in-report-builder.md)。  
  
  
  
##  <a name="Credentials"></a> 凭据  
 执行以下操作时需要提供凭据：运行查询、本地预览报表以及从报表服务器预览报表。  
  
 报表发布后，您可能需要更改数据源的凭据，以使报表在报表服务器上运行时，用于检索数据的权限有效。  
  
 有关详细信息，请参阅 [在报表生成器中指定凭据](../specify-credentials-in-report-builder.md)。  
  
  
  
##  <a name="Query"></a> 查询  
 使用报表模型查询设计器可按照交互方式指定实体、字段和查询筛选器。 模型中的实体和字段将成为在“报表数据”窗格中显示的数据集字段集合。  
  
  
  
##  <a name="Parameters"></a> Parameters  
 若要添加报表参数，请在报表模型查询设计器中创建带提示符的筛选器。  
  
 报表参数是用可能需要修改的默认属性值创建的。 默认情况下，每个报表参数的数据类型均为 **Text**。 如果基础数据属于其他数据类型，则必须更改参数的数据类型。  
  
 有关详细信息，请参阅 [报表参数（报表生成器和报表设计器）](../report-design/report-parameters-report-builder-and-report-designer.md)的详细信息。  
  
  
  
##  <a name="Remarks"></a> 注释  
 不是所有的报表传递模式都受到此数据访问接口的支持。 此数据处理扩展插件不支持通过数据驱动订阅传递报表。 有关详细信息，请参阅[使用外部数据源提供订阅方数据（数据驱动订阅）](../subscriptions/use-an-external-data-source-for-subscriber-data-data-driven-subscription.md)。  
  
  
  
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
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [联机丛书](https://go.microsoft.com/fwlink/?linkid=121312)中 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 文档中的 [Reporting Services 支持的数据源 (SSRS) ](../create-deploy-and-manage-mobile-and-paginated-reports.md)。  
 提供有关每个数据扩展插件的平台和版本支持的详细信息。  
  
  
  
## <a name="see-also"></a>请参阅  
 [查找、查看和管理报表（报表生成器和 SSRS）](../report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [报表参数（报表生成器和报表设计器）](../report-design/report-parameters-report-builder-and-report-designer.md)   
 [对数据进行筛选、分组和排序（报表生成器和 SSRS）](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [表达式（报表生成器和 SSRS）](../report-design/expressions-report-builder-and-ssrs.md)  
  
  
