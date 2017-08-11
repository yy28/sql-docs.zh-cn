---
title: "验证报表运行情况 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- auditing [Reporting Services]
- verifying report execution
- logs [Reporting Services], verifying report run
- report execution data [Reporting Services]
- status information [Reporting Services]
- report processing [Reporting Services], verifying execution
- checking report execution
ms.assetid: 18a98f2f-6b40-454e-9b37-568ed1a96458
caps.latest.revision: 37
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 97015ca82fd8a58c3c5cd351b2f7379711d65aa1
ms.contentlocale: zh-cn
ms.lasthandoff: 08/09/2017

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
|作为报表快照运行的报表。|在“内容”页上。 有关详细信息，请参阅[内容页 &#40;报表管理器 &#41;](http://msdn.microsoft.com/library/6b16869b-158a-4934-9c85-bee934b35378).|1) 找到包含该报表的文件夹。<br /><br /> 2) 在“详细信息”视图中设置该文件夹。<br /><br /> 3） 请注意日期和时间在**时运行**列。|  
|报表历史记录中的快照。|在“历史记录”属性页上。 有关详细信息，请参阅[快照选项属性页 &#40;报表管理器 &#41;](http://msdn.microsoft.com/library/f6641f59-5267-4f57-8957-63b93d1a9679).|1) 打开该报表。<br /><br /> 2） 单击**属性**页。<br /><br /> 3） 单击**历史记录**选项卡。<br /><br /> 4） 请注意日期和时间在**时运行**列。|  
|缓存的报表。|在用于创建和刷新该缓存报表的计划中。|1) 打开该报表。<br /><br /> 2） 单击**属性**页。<br /><br /> 3） 单击**执行**选项卡。<br /><br /> 4) 打开该计划。|  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services 日志文件和来源](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)   
 [设置报表处理属性](../../reporting-services/report-server/set-report-processing-properties.md)   
 [报表管理器 &#40;SSRS 本机模式 &#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)  
  
  
