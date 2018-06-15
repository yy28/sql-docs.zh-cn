---
title: 将列添加到挖掘结构 |Microsoft 文档
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4c09d4b263dc4e4274888f6cbd8bf1f27103dd8b
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34016284"
---
# <a name="add-columns-to-a-mining-structure"></a>向挖掘结构中添加列
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  在数据挖掘向导中定义了挖掘结构后，可以使用 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 中的数据挖掘设计器在挖掘结构中添加列。 您可以添加用于定义挖掘结构的数据源视图中存在的任何列。  
  
> [!NOTE]  
>  您可以向挖掘结构中添加列的多个副本；不过，应避免在同一个模型中使用列的多个实例，以避免源列和派生列之间发生错误关联。  
  
### <a name="to-add-a-column-to-a-mining-structure"></a>向挖掘结构中添加列  
  
1.  在数据挖掘设计器中选择 **“挖掘结构”** 选项卡。  
  
2.  右键单击挖掘结构并选择“添加列”。  
  
     **“选择列”** 对话框将打开。  
  
3.  在 **“源表”** 下，从数据源视图中选择列所在的表。  
  
4.  在 **“源列”** 下，选择要添加到挖掘结构中的列。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
> [!NOTE]  
>  如果您添加的列已经存在，则结构中将会包含一个副本，并在其名称后追加“1”。 在挖掘结构列的 **“名称”** 属性中键入新名称，可以更改已复制列的名称，使之更具说明性。  
  
## <a name="see-also"></a>另请参阅  
 [挖掘结构任务和操作指南](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md)  
  
  
