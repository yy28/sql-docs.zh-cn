---
title: "将列添加到挖掘结构 |Microsoft 文档"
ms.custom: 
ms.date: 03/13/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
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
ms.openlocfilehash: 5dfeade08192456bae474b633af9bd401dfa0fde
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="add-columns-to-a-mining-structure"></a>向挖掘结构中添加列
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]使用数据挖掘设计器中[!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]将列添加到挖掘结构之后在数据挖掘向导中定义。 您可以添加用于定义挖掘结构的数据源视图中存在的任何列。  
  
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
  
  
