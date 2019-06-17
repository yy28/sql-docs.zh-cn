---
title: 通知 （存储选项对话框) (Analysis Services-多维数据) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.partitiondesigner.partitionstoragesettings.setstorageoptions.notifications.f1
ms.assetid: 5675cdbf-bfaa-4b6e-b716-31b8e9da72b4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 23845118c4c202db781fe325c4afc2402ceee271
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66072196"
---
# <a name="notifications-storage-options-dialog-box-analysis-services---multidimensional-data"></a>通知（“存储选项”对话框）（Analysis Services - 多维数据）
  可以使用 **中的** “存储选项” **对话框上的** “通知” [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 选项卡，设置维度、多维数据集、度量值组或分区的通知方法和相关设置。  
  
> [!NOTE]  
>  您必须熟悉存储模式和主动缓存功能，才可以修改这些设置。 有关详细信息，请参阅[主动缓存（分区）](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)。  
  
## <a name="options"></a>选项  
  
|术语|定义|  
|----------|----------------|  
|**存储模式**|选择对象要使用的存储模式。<br /><br /> **MOLAP**<br /> 对象使用多维 OLAP (MOLAP) 存储。<br /><br /> **HOLAP**<br /> 对象使用混合 OLAP (HOLAP) 存储。<br /><br /> **ROLAP**<br /> 对象使用关系 OLAP (ROLAP) 存储。|  
|**启用了主动缓存**|启用主动缓存。<br /><br /> 注意：如果未选择此选项，所有选项除外**存储模式**处于禁用状态。|  
|**SQL Server**|使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 上的专用跟踪机制，可以标识对象的基础表的更改。|  
|**指定跟踪表**|为对象指定要跟踪的基础表，然后键入表的列表并使用分号 (;) 字符进行分隔，或单击省略号按钮 ( **...** ) 以打开“关系对象”  对话框并选择要跟踪的表。 有关详细信息，请参阅[“关系对象”对话框（Analysis Services - 多维数据）](relational-objects-dialog-box-analysis-services-multidimensional-data.md)。<br /><br /> 如果未选中此选项，在满足特定要求的情况下， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 将尝试为对象确定要跟踪的基础表的列表。 有关这些要求的详细信息，请参阅[主动缓存（分区）](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)。|  
|**启动的客户端**|选择此选项可以使用 XML for Analysis (XMLA) 命令 `NotifyTableChange`，以标识对象的基础表的更改。 如果计划使用基于客户端的通知过程，通常应选择此选项。|  
|**指定跟踪表**|选择此选项可以为对象指定要跟踪的基础表，然后键入表的列表并使用分号 (;) 字符进行分隔，或单击省略号按钮 ( **...** ) 以打开“关系对象”  对话框并选择要跟踪的表。 有关详细信息，请参阅[“关系对象”对话框（Analysis Services - 多维数据）](relational-objects-dialog-box-analysis-services-multidimensional-data.md)。<br /><br /> 如果未选中此选项，在满足特定要求的情况下， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 将尝试为对象确定要跟踪的基础表的列表。 有关这些要求的详细信息，请参阅[主动缓存（分区）](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)。|  
|**按计划的轮询**|使用轮询机制，通过对相应对象的基础表运行一系列查询以标识更改。|  
|**轮询间隔**|指定时间间隔和单位， [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 在此时间段之后才会执行轮询网格中定义的轮询查询和处理查询。|  
|**启用增量更新**|基于一组专用于只标识追加数据的轮询查询和处理查询，增量更新对象的 MOLAP 缓存。 如果选择此选项，轮询查询将与数据源视图中的一个表标识符相关联。 随后，系统会使用处理查询将轮询查询的当前值与上次所执行轮询查询的存储值进行比较，以标识更改。<br /><br /> 如果未选择此选项，则会完全更新 MOLAP 缓存。 系统将使用轮询查询来标识已发生更改，而不需要使用处理查询或表标识符。|  
|**轮询网格**|包含 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 使用的轮询查询、处理查询和表标识符，这些查询及标识符用于轮询数据源和标识对象基础表的更改。 该网格包含以下列：<br /><br /> **轮询查询**：键入按轮询间隔执行的用于标识对象更改的单独查询，或单击省略号按钮 ( **...** ) 以打开“创建轮询查询”  对话框并定义单独查询。 有关详细信息，请参阅[“创建轮询查询”对话框（Analysis Services - 多维数据）](create-polling-query-dialog-box-analysis-services-multidimensional-data.md)。 如果选择了 **“启用增量更新”** ，轮询查询应返回标识添加到 **“表”** 中所标识表的最后一条记录的值。 如果未选择 **“启用增量更新”** ，轮询查询应返回标识表中当前记录数的值。<br /><br /> **处理查询**：键入按轮询间隔执行的用于从“表”  中所标识表检索新记录的查询，或单击省略号按钮 ( **...** ) 以打开“创建处理查询”  对话框并定义查询。 有关详细信息，请参阅[“创建处理查询”对话框（Analysis Services - 多维数据）](create-processing-query-dialog-box-analysis-services-multidimensional-data.md)。 查询应进行参数化以接受两个参数的以前的值中查询返回的**轮询查询**中的查询返回的当前值和**轮询查询**-可用于标识和提取在轮询期间已添加的记录。 请注意，只有在选择了“启用增量更新”  时，才会启用此选项。<br /><br /> **表**：键入“轮询查询”  中指定查询要跟踪其最后一条记录的表的标识符，或单击省略号按钮 ( **...** ) 以打开“查找表”  对话框并选择相应的表。 有关详细信息，请参阅[“查找表”对话框（Analysis Services - 多维数据）](find-table-dialog-box-analysis-services-multidimensional-data.md)。|  
  
## <a name="see-also"></a>请参阅  
 [存储选项对话框的&#40;Analysis Services-多维数据&#41;](storage-options-dialog-box-analysis-services-multidimensional-data.md)  
  
  
