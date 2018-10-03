---
title: 验证报表运行情况 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- auditing [Reporting Services]
- verifying report execution
- logs [Reporting Services], verifying report run
- report execution data [Reporting Services]
- status information [Reporting Services]
- report processing [Reporting Services], verifying execution
- checking report execution
ms.assetid: 18a98f2f-6b40-454e-9b37-568ed1a96458
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: e8bddd67dca8a97d0279b002784c74e9666e5a15
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48076517"
---
# <a name="verifying-a-report-run"></a>验证报表运行情况
  若要查看报表处理状态的有关信息，则可以使用日志文件或参考在报表管理器中随报表显示的状态信息。  
  
## <a name="sources-of-report-execution-data"></a>报表执行数据的源  
 报表执行日志提供了有关报表执行情况的综合信息，其中包括：报表的名称、运行报表的用户的名称、报表执行时间以及用于分发报表的传递扩展插件。 若要查看和分析此数据，可以将报表执行日志复制到便于查询和报告的数据库表中。  
  
 日志文件包含有关报表执行情况和其他服务器活动的许多条目。 由于日志文件包含大量数据，因此，如果您只想验证上一次运行报表的时间，则可以使用报表管理器。 如果需要其他信息，就必须查看日志文件。  
  
> [!NOTE]  
>  报表管理器不显示按需运行的报表的处理时间。  
  
 下表对如何查看各种报表的处理日期和时间进行了说明：  
  
|报表类型|日期和时间信息所在位置|查看信息所需操作|  
|-----------------------------|-----------------------------------------------|-----------------------------------------------|  
|作为报表快照运行的报表。|在“内容”页上。 有关详细信息，请参阅[“内容”页（报表管理器）](../contents-page-report-manager.md)。|1) 找到包含该报表的文件夹。<br />2) 在“详细信息”视图中设置该文件夹。<br />3) 3) 请注意日期和时间**时运行**列。|  
|报表历史记录中的快照。|在“历史记录”属性页上。 有关详细信息，请参阅[“快照选项”属性页（报表管理器）](../snapshot-options-properties-page-report-manager.md)。|1) 打开该报表。<br />2) 单击“属性”页。<br />3) 单击“历史记录”选项卡。<br />4) 请注意“运行时间”列中的日期和时间。|  
|缓存的报表。|在用于创建和刷新该缓存报表的计划中。|1) 打开该报表。<br />2) 单击“属性”页。<br />3) 单击“执行”选项卡。<br />4) 打开该计划。|  
  
## <a name="see-also"></a>请参阅  
 [Reporting Services 日志文件和来源](../report-server/reporting-services-log-files-and-sources.md)   
 [设置报表处理属性](set-report-processing-properties.md)   
 [报表管理器（SSRS 本机模式）](../report-manager-ssrs-native-mode.md)  
  
  
