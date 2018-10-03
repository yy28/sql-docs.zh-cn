---
title: 使用外部数据源提供订阅方数据（数据驱动订阅）| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- subscriber data sources [Reporting Services]
- subscriptions [Reporting Services], external data sources
- query-based subscriptions [Reporting Services]
- external data sources [Reporting Services]
- data-driven subscriptions
- data sources [Reporting Services], subscriptions
ms.assetid: 1cade8ec-729c-4df8-a428-e75c9ad86369
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: f0112a4a9ae89dbfc2aedad38c16056a4d246964
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48174707"
---
# <a name="use-an-external-data-source-for-subscriber-data-data-driven-subscription"></a>使用外部数据源提供订阅方数据（数据驱动订阅）
  在数据驱动订阅中，动态订阅数据是由从外部数据源检索数据的查询或命令提供的。 可以从满足数据驱动订阅处理要求的任何支持数据源中检索订阅数据。 查询或命令语法必须对随报表服务器安装的数据处理扩展插件有效。  
  
## <a name="data-processing-requirements"></a>数据处理要求  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 使用数据处理扩展插件检索订阅数据。 建议的数据源类型包括以下各项：  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 关系数据库  
  
-   Oracle 数据库  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 多维和数据挖掘数据源  
  
-   XML 数据源  
  
     使用 XML 数据处理扩展插件处理订阅服务器数据时，请确保在订阅中增加查询超时设置。 XML 数据处理扩展插件使用毫秒（而不是秒）来表示查询超时值。 如果您没有增加超时值，则订阅可能会因处理时间不足而失败。  
  
     配置与订阅服务器数据源的连接时，应避免使用 **“不需要凭据”** 选项。 在运行时使用 XML 数据处理扩展插件检索订阅数据时，建议使用存储的凭据。  
  
 您可能可以使用其他支持的数据源类型，但并不能保证所有的数据源类型都能正常发挥作用。 例如，以下数据源类型不能用于订阅服务器数据：  
  
-   SAP Netweaver BI 数据源  
  
-   报表模型  
  
 如果你有要在数据驱动订阅中使用的自定义数据处理扩展插件，则它必须实现 <xref:Microsoft.ReportingServices.DataProcessing.IDbCommand> 和 <xref:Microsoft.ReportingServices.DataProcessing.IDataReader> 接口。 数据处理扩展插件必须支持仅限架构的查询执行。 此查询用于在设计时检索列元数据，以使用户可以将列映射到订阅定义中的传递选项和报表参数。 仅限架构的查询执行发生在用户定义订阅的初期阶段。  
  
## <a name="query-requirements"></a>查询要求  
 创建用于检索订阅数据的查询时，请牢记以下要点：  
  
-   只能为订阅创建一个查询。  
  
-   查询必须返回所有要用于传递选项和用于指定报表参数的值。  
  
-   报表服务器将为结果集中的每一行都创建一个报表传递。 如果结果集包含三百多行，则报表服务器将尝试传递三百个报表。  
  
## <a name="setting-delivery-options-using-variable-data-from-a-subscriber-database"></a>使用订阅服务器数据库中的变量数据设置传递选项  
 可以使用订阅服务器数据库中的数据为每个接收者自定义传递选项。 您所使用的传递扩展插件的类型将确定哪些选项是可用的。 如果正在使用报表服务器电子邮件传递扩展插件，则该查询应包含每个订阅方的电子邮件别名。 如果正在使用文件共享传递，则订阅方数据应包含可用于创建订阅方特定的报表文件或提供传递目标的值。 有关详细信息，请参阅[File Share Delivery in Reporting Services](file-share-delivery-in-reporting-services.md)并[Reporting Services 中的电子邮件传递](e-mail-delivery-in-reporting-services.md)。  
  
## <a name="passing-parameter-values-from-the-subscriber-database-to-the-report"></a>将参数值从订阅服务器数据库传递到报表  
 如果要为参数化报表创建数据驱动订阅，则可以使用变量参数值来自定义每个报表的输出。 例如，订阅服务器数据库可能包含雇员标识号、雇用日期、职务和办公地点信息，这些信息可用来筛选报表数据。 如果报表接受基于这些数据或其他可用列数据的参数，则可以将参数映射到相应的列。  
  
 将订阅方字段映射到报表参数时，请确保数据类型和列长度相符。 如果数据类型不匹配，则在订阅处理过程中将会出现错误。 若要了解有关使用参数化报表中订阅方数据的详细信息，请参阅[创建数据驱动订阅（SSRS 教程）](../create-a-data-driven-subscription-ssrs-tutorial.md)。  
  
## <a name="modifying-the-subscriber-data-source"></a>修改订阅方数据源  
 对订阅方数据源进行以下修改将会阻止订阅运行：  
  
-   删除订阅中引用的列。  
  
-   修改数据源的表结构。  
  
-   更改数据类型和其他列属性。  
  
 如果执行了上述任何更改，则必须更新订阅。  
  
## <a name="see-also"></a>请参阅  
 [创建、 修改和删除数据驱动订阅](data-driven-subscriptions.md)   
 [数据驱动订阅](data-driven-subscriptions.md)   
 [订阅和传递 (Reporting Services)](subscriptions-and-delivery-reporting-services.md)  
  
  
