---
title: "将列添加到挖掘结构 |Microsoft 文档"
ms.custom: 
ms.date: 03/13/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mining structures [Analysis Services], columns
- columns [data mining], mining structure columns
- adding columns
ms.assetid: 3f879344-9f66-4178-851a-e8c5ccccf4cb
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4d01bf68958891379b00f770e38065d400b407bb
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="add-columns-to-a-mining-structure"></a>向挖掘结构中添加列
  在数据挖掘向导中定义了挖掘结构后，可以使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中的数据挖掘设计器在挖掘结构中添加列。 您可以添加用于定义挖掘结构的数据源视图中存在的任何列。  
  
> [!NOTE]  
>  您可以向挖掘结构中添加列的多个副本；不过，应避免在同一个模型中使用列的多个实例，以避免源列和派生列之间发生错误关联。  
  
### <a name="to-add-a-column-to-a-mining-structure"></a>向挖掘结构中添加列  
  
1.  在数据挖掘设计器中选择 **“挖掘结构”** 选项卡。  
  
2.  右键单击挖掘结构并选择“添加列”。  
  
     **“选择列”** 对话框将打开。  
  
3.  在 **“源表”**下，从数据源视图中选择列所在的表。  
  
4.  在 **“源列”**下，选择要添加到挖掘结构中的列。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
> [!NOTE]  
>  如果您添加的列已经存在，则结构中将会包含一个副本，并在其名称后追加“1”。 在挖掘结构列的 **“名称”** 属性中键入新名称，可以更改已复制列的名称，使之更具说明性。  
  
## <a name="see-also"></a>另请参阅  
 [挖掘结构任务和操作指南](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md)  
  
  
