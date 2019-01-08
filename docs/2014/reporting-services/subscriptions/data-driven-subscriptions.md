---
title: 数据驱动订阅 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], data-driven
- data-driven subscriptions
ms.assetid: ba009f62-0d4f-45e7-a27c-36fd5f0cd3a8
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 71ab6239172ea39a8adcee9ca017a5408079a8d5
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/13/2018
ms.locfileid: "53357149"
---
# <a name="data-driven-subscriptions"></a>数据驱动订阅
  数据驱动订阅提供了一种使用动态订阅数据的方式，这些数据是在运行时从外部数据源中检索的。 数据驱动订阅还可以使用定义订阅时指定的静态文本和默认值。 可以使用数据驱动订阅来执行以下操作：  
  
-   向可以变动的订阅方列表分发报表。 例如，您可以使用数据驱动订阅在订阅方会逐月变化的大型单位中分发报表，也可以使用其他条件在一组现有用户中确定组成员身份。  
  
-   使用在运行时检索的报表参数值筛选报表输出。  
  
-   更改报表输出格式和每个报表传递的传递选项。  
  
 数据驱动订阅由多个部分组成。 数据驱动订阅所涉及的固定方面是在创建订阅时定义的，其中包括以下内容：  
  
-   为其定义订阅的报表（订阅始终与单个报表相关联）。  
  
-   用于分发报表的传递扩展插件。 可以指定报表服务器电子邮件传递、文件共享传递、用于预加载缓存的 Null 传递提供程序或自定义传递扩展插件。 不能在单个订阅中指定多个传递扩展插件。  
  
-   订阅方数据源。 定义订阅时，您必须为包含订阅方数据的数据源指定连接字符串。 不能在运行时动态指定订阅方数据源。  
  
-   定义订阅时必须指定用于选择订阅方数据的查询。 不能在运行时更改该查询。  
  
 数据驱动订阅中使用的动态值是在处理订阅时获取的。 在订阅中可能使用的变量数据示例包括订阅方名称、电子邮件地址、首选的报表输出格式或任何对报表参数有效的值。 若要在数据驱动订阅中使用动态值，可以在查询中为特定传递选项和报表参数返回的字段之间定义映射。 每次处理订阅时，都将从订阅方数据源中检索变量数据。  
  
## <a name="requirements-for-using-data-driven-subscriptions"></a>使用数据驱动订阅的要求  
 数据驱动订阅功能并不是在所有的版本中都可用。 对于在运行时可用于检索订阅数据的数据源种类还有一些限制。 以下列表提供了有关这些要求的详细信息：  
  
-   有关支持数据驱动订阅功能的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本的详细信息，请参阅 [SQL Server 2012 各个版本支持的功能](https://go.microsoft.com/fwlink/?linkid=232473) (https://go.microsoft.com/fwlink/?linkid=232473)。  
  
-   对于订阅数据，请选择可为报表服务器提供架构信息的数据源。 支持的数据源类型的示例包括 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 关系数据、Oracle、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包数据、ODBC 数据源以及 OLE DB 数据源。 有关订阅方数据源要求的详细信息，请参阅 [使用外部数据源提供订阅方数据（数据驱动订阅）](use-an-external-data-source-for-subscriber-data-data-driven-subscription.md)。  
  
## <a name="working-with-data-driven-subscriptions"></a>处理数据驱动订阅  
 以下主题介绍有关数据驱动订阅的详细信息：  
  
|主题|Description|  
|------------|-----------------|  
|[创建、修改和删除数据驱动订阅](data-driven-subscriptions.md)|介绍如何创建、修改和删除数据驱动订阅。|  
|[使用外部数据源提供订阅方数据（数据驱动订阅）](use-an-external-data-source-for-subscriber-data-data-driven-subscription.md)|介绍有关可用于数据驱动订阅的数据源的信息。|  
|[创建数据驱动订阅（SSRS 教程）](../create-a-data-driven-subscription-ssrs-tutorial.md)|逐步介绍如何创建数据驱动订阅。|  
|[缓存报表 (SSRS)](../report-server/caching-reports-ssrs.md)|介绍如何对数据驱动订阅使用 Null 传递提供程序来预先加载缓存。|  
  
## <a name="see-also"></a>请参阅  
 [订阅和传递 (Reporting Services)](subscriptions-and-delivery-reporting-services.md)   
 [“创建数据驱动订阅”页（报表管理器）](../create-data-driven-subscription-page-report-manager.md)   
 [预加载缓存（报表管理器）](../report-server/preload-the-cache-report-manager.md)  
  
  
