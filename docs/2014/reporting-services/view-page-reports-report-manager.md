---
title: 查看页上，报表 （报表管理器） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 4874ba29-429b-4dd4-a8cb-d4f087237dc2
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 8a2697af9ede2b6b72e7f08efd88822101c51d53
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48102797"
---
# <a name="view-page-reports-report-manager"></a>报表的“视图”页（报表管理器）
  使用报表的“视图”页可以查看报表。 在报表管理器中最初打开报表时，报表采用 HTML 格式。 HTML 报表包括一个显示在报表顶部的报表工具栏，通过它可以导航报表页、在报表中搜索或将报表导出到不同格式。 下图显示了报表工具栏。  
  
 ![报表工具栏](media/htmlviewer-toolbar.gif "Report toolbar")  
报表工具栏  
  
 在 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]中，可将报表配置为按需运行或从报表执行快照中运行。 如果报表按需运行，则每次打开报表时都会进行所有数据处理和报表处理。 如果要查看的报表被配置为作为报表执行快照来运行，则会在创建快照时进行数据处理。  
  
## <a name="exporting-reports"></a>导出报表  
 并非所有报表功能在所有导出格式中都可用。 如果将 HTML 报表导出到另一种格式，则可能会看到报表外观上的一些差异。 此外，如果报表中包括交互功能（例如超链接、书签或文档结构图），这些功能在新格式中可能不可用或无法正常使用。  
  
## <a name="generating-data-feeds-from-report-data"></a>基于报表数据生成数据馈送  
 可以从报表生成数据馈送。 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] Atom 呈现扩展插件可生成两个 Atom 兼容文档：一个 Atom 服务文档，其中列出报表提供的数据馈送和包含报表数据的数据馈送。 数据馈送由 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 以标准化的 Atom 1.0 兼容格式生成，这种格式是可读的，并可以与使用 Atom 兼容数据馈送的应用程序进行交换。 例如， [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] 客户端可以使用从报表生成的数据馈送。  
  
## <a name="running-parameterized-reports"></a>运行参数化报表  
 如果报表包含输入字段和 **“查看报表”** 按钮，则该报表为参数化报表。 若要查看参数化报表，需要提供相应的值以用于运行报表。  
  
> [!NOTE]  
>  并非所有 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]版本都提供报表执行快照和某些导出格式。 有关详细信息，请参阅 [Features Supported by the Editions of SQL Server 2014](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
## <a name="see-also"></a>请参阅  
 [报表管理器&#40;SSRS 本机模式&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [报表管理器的 F1 帮助](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
