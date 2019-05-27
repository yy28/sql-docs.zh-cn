---
title: 远程分区-高级设置对话框 (Analysis Services-多维数据) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.advancedrestoresettings.f1
ms.assetid: a03bb7e1-efaf-47c8-b0ee-f3e4438311cb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1ca3f12ff53c4291d8bbe7c8eb97ce8e47172ea3
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66070381"
---
# <a name="remote-partitions---advanced-settings-dialog-box-analysis-services---multidimensional-data"></a>“远程分区 - 高级设置”对话框（Analysis Services - 多维数据）
  可以使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中的“远程分区 - 高级设置”对话框，编辑高级设置（如代表维护远程分区的远程 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库的数据源连接字符串），以及使用“还原数据库”对话框将远程分区从远程备份文件还原到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库。 在选择“还原远程分区”选项之后，通过单击某个远程分区的省略号按钮 (**...**)，可以从“还原数据库”对话框的“分区”页显示“远程分区 - 高级设置”对话框。  
  
## <a name="options"></a>选项  
  
|术语|定义|  
|----------|----------------|  
|**数据源名称**|显示表示管理所列远程分区的远程 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库的数据源名称。|  
|**“备份文件”**|显示包含要为所列远程分区还原的数据的远程备份文件名称。<br /><br /> 注意：如果在指定了远程备份文件，会看到任何备份文件**备份文件**上的列**分区**页**Restore Database**对话框。|  
|**连接字符串**|显示在 **“数据源名称”** 中显示的数据源的连接字符串。|  
|**编辑**|单击此项可以显示 **“数据链接属性”** 对话框，并编辑连接字符串中所包含的属性。|  
|**分区列表**|选择此选项可以指定要还原远程分区的其他位置。 注意：只有在多维数据集中为远程分区指定了除默认位置之外的位置后，才可以更改远程分区的还原文件夹。 下面的网格（选择此选项后启用）用于指定每个远程分区的还原文件夹：<br /><br /> **多维数据集**：显示包含远程分区的多维数据集的名称。<br /><br /> **MeasureGroup**：显示包含远程分区的度量值组的名称。<br /><br /> **分区**：显示远程分区的名称。<br /><br /> **大小 (MB)**：显示远程分区的大小 (MB)。<br /><br /> **原始文件夹**：显示存储远程分区的原始文件夹的名称。<br /><br /> **还原文件夹**：键入远程分区的还原文件夹的名称，或单击省略号按钮 (**...**) 以显示“查找远程文件夹”对话框，再选择要使用的文件夹的路径。 有关“查找远程文件夹”对话框的详细信息，请参阅[“查找远程文件夹”对话框（Analysis Services - 多维数据）](browse-for-remote-folder-dialog-box-analysis-services-multidimensional-data.md)。|  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 设计器和对话框&#40;多维数据&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [分区&#40;还原数据库对话框&#41; &#40;Analysis Services-多维数据&#41;](partitions-restore-database-dialog-box-analysis-services-multidimensional-data.md)   
 [备份和还原 Analysis Services 数据库](multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  
