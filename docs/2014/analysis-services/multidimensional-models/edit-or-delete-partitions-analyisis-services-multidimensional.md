---
title: 编辑或删除分区 (Analyisis Services-多维) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- modifying partitions
- partitions [Analysis Services], modifying
ms.assetid: fb7a64ca-d021-4926-b92d-83476fbc40a3
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 693550400db63b73b29d01a7a9d198d5924893dc
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36123921"
---
# <a name="edit-or-delete-partitions-analyisis-services---multidimensional"></a>编辑或删除分区（Analysis Services - 多维）
  多维数据集分区可在 **中使用多维数据集设计器中的** “分区” [!INCLUDE[ssBIDevStudio](../../../includes/ssbidevstudio-md.md)]选项卡来修改。 **“分区”** 选项卡列出了多维数据集中的所有度量值组的分区。 它还列出了已启用写回的写回分区。  
  
 若要编辑任何度量值组的分区，请在 **“分区”** 选项卡上展开该度量值组。度量值组的分区按照序号以表的形式列出，表中使用了下表中列出的列。  
  
 必须在源多维数据集中编辑链接度量值组的设置。  
  
 当您将源分区合并到目标分区时，将自动删除分区。 合并后将删除被指定为“源”的分区。 您也可以在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 中或在 [!INCLUDE[ssBIDevStudio](../../../includes/ssbidevstudio-md.md)]中的“分区”选项卡中手动删除分区。 右键单击并选择“删除”。 请记住，删除分区时也会同时删除数据和聚合。 作为预防措施，请确保您具有数据库的近期备份版本，以备您在以后需要撤消此步骤时使用。  
  
> [!NOTE]  
>  或者，您也可以使用可自动执行生成、合并和删除分区任务的 XMLA 脚本。 XMLA 脚本可在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]中或在作为计划任务运行的自定义 SSIS 包中创建和执行。 有关详细信息，请参阅 [Automate Analysis Services Administrative Tasks with SSIS](../instances/automate-analysis-services-administrative-tasks-with-ssis.md)。  
  
## <a name="partition-source"></a>分区源  
 为分区指定源表或命名查询。 若要更改源表，请单击该单元，再单击浏览 (**...**) 按钮。  
  
 ![在分区窗格中的源列](../media/ssas-partitionsource.png "在分区窗格中的源列")  
  
 如果分区基于一个查询，则单击浏览 (**...**) 按钮来编辑该查询。 这将编辑分区的 **“源”** 属性。 有关详细信息，请参阅 [更改分区源以使用不同的事实数据表](change-a-partition-source-to-use-a-different-fact-table.md)。  
  
 您可以指定数据源视图中与初始源表（在用于检索数据的外部数据源中）具有相同结构的表。 源可位于多维数据集数据库的任意数据源或数据源视图中。  
  
## <a name="storage-settings"></a>存储设置  
 在多维数据集设计器中的“分区”选项卡上，可以单击 **“存储设置”** 为 MOLAP 、ROLAP 或 HOLAP 存储选择一个标准设置，也可以为存储模式和主动缓存配置自定义设置。 默认选择是 MOLAP，因为它能够提供最佳查询性能。 有关每个设置的详细信息，请参阅[设置分区存储（Analysis Services - 多维）](set-partition-storage-analysis-services-multidimensional.md)。  
  
 可以为多维数据集中每个度量值组的每一个分区分别配置存储。 也可以为多维数据集或度量值组配置默认存储设置。 存储是在多维数据集向导中的 **“分区”** 选项卡中进行配置的。  
  
## <a name="see-also"></a>请参阅  
 [创建和管理本地分区&#40;Analysis Services&#41;](create-and-manage-a-local-partition-analysis-services.md)   
 [设计聚合&#40;Analysis Services-多维&#41;](designing-aggregations-analysis-services-multidimensional.md)   
 [在 Analysis Services 中合并分区&#40;SSAS-多维&#41;](merge-partitions-in-analysis-services-ssas-multidimensional.md)  
  
  