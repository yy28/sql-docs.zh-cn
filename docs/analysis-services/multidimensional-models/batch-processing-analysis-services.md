---
title: 批处理 (Analysis Services) |Microsoft 文档
ms.custom: ''
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- batches [Analysis Services]
ms.assetid: ba4dcf72-0667-41d0-816b-ab8ff9a7d9cb
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ec94963644de42f6fd07da60c16f2f314f168e41
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="batch-processing-analysis-services"></a>批处理 (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]在[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]，你可以使用批处理命令将多个处理命令发送到单个请求中的服务器。 通过批处理，您可以控制以什么顺序来处理哪些对象。 此外，批可以作为一系列独立作业运行，也可以作为一个事务运行，如果事务中的某个进程失败，则会导致整批回滚。  
  
 批处理通过合并和减少提交更改所用的时间，最大限度地提高数据可用性。 在完全处理一个维度时，任何使用该维度的分区都会标记为未处理。 因此，包含未处理分区的多维数据集不可用于浏览。 可以通过批处理作业将维度和受影响的分区一起处理来解决该问题。 将批处理作业作为事务来运行，可确保该事务中包括的所有对象在处理完成前仍可用于查询。 由于事务提交更改时，会对受影响的对象放置锁，因此会使这些对象暂时不可用；但是，用于提交更改的总时间比单独处理对象的时间要短。  
  
 本主题中的过程展示了完全处理维度和分区的步骤。 批处理还包括其他处理选项，例如增量处理。 若要这些过程能够正常工作，应使用至少包括两个维度和一个分区的现有 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库。  
  
 本主题包含以下各节：  
  
 [在 SQL Server Data Tools 中执行批处理](#bkmk_ssdt)  
  
 [在 Management Studio 中使用 XMLA 执行批处理](#bkmk_xmla)  
  
##  <a name="bkmk_ssdt"></a> 在 SQL Server Data Tools 中执行批处理  
 在 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]中处理对象前，必须部署包含对象的项目。 有关详细信息，请参阅[部署 Analysis Services 项目 (SSDT)](../../analysis-services/multidimensional-models/deploy-analysis-services-projects-ssdt.md)。  
  
1.  打开 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]。  
  
2.  打开已部署的项目。  
  
3.  在解决方案资源管理器中，在已部署项目下，展开 **“维度”** 文件夹。  
  
4.  按住 Ctrl 键，单击 **“维度”** 文件夹中列出的每个维度。  
  
5.  右键单击所选维度，再单击“处理”。  
  
6.  按住 Ctrl 键，单击 **“对象列表”**中列出的每个维度。  
  
7.  右键单击所选的维度并选择“处理全部”。  
  
8.  若要自定义批处理作业，请单击 **“更改设置”**。  
  
9. 在 **“处理选项”**下，进行下列设置：  
  
    -   将**“处理顺序”** 设置为 **“按顺序”**，将 **“事务模式”** 设置为 **“一项事务”**。  
  
    -   **“写回表选项”** 设置为 **“使用现有的”**。  
  
    -   在 **“受影响的对象”**下，选中 **“处理受影响的对象”** 复选框。  
  
10. 单击 **“维度键错误”** 选项卡。确保已选中 **“使用默认错误配置”** 。  
  
11. 单击 **“确定”** 以关闭 **“更改设置”** 屏幕。  
  
12. 在 **“处理对象”** 屏幕内单击 **“运行”** 以启动处理作业。  
  
13. 当 **“状态”** 框显示 **“处理已成功”**时，单击 **“关闭”**。  
  
14. 单击 **“处理对象”** 屏幕上的 **“关闭”** 。  
  
##  <a name="bkmk_xmla"></a> 在 Management Studio 中使用 XMLA 执行批处理  
 您可以创建一个执行批处理的 XMLA 脚本。 首先在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中为每个对象生成一个 XMLA 脚本，然后将这些脚本并入以交互方式运行或在计划任务内运行的一个 XMLA 查询。  
  
 有关分步说明，请参阅 **使用 SQL Server 代理来计划 SSAS 管理任务** 中的 [示例 2](../../analysis-services/instances/schedule-ssas-administrative-tasks-with-sql-server-agent.md)  
  
## <a name="see-also"></a>另请参阅  
 [处理多维模型 (Analysis Services)](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)  
  
  
