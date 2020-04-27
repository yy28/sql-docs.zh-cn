---
title: 更改 DirectQuery 分区（SSAS 表格） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: f9df1e66-dd23-41b4-95eb-af110d10eda4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1eb0b6349eac28bbd2abc22b9483ef74edf1bf33
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66088184"
---
# <a name="change-the-directquery-partition-ssas-tabular"></a>更改 DirectQuery 分区（SSAS 表格）
  因为在一个表中只能有一个分区可以指定为 DirectQuery 分区，所以，默认情况下，Analysis Services 使用在该表中创建的第一个分区。 在模型项目创作过程中，您可以通过使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中的“分区管理器”对话框来更改 DirectQuery 分区。 对于部署的模型，您可以通过使用 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]来更改 DirectQuery 分区。  
  
### <a name="change-the-directquery-partition-for-a-tabular-model-project"></a>更改表格模型项目的 DirectQuery 分区  
  
1.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]的模型设计器中，单击包含已分区表的表（选项卡）。  
  
2.  单击 **“表”** 菜单，然后单击 **“分区”**。  
  
3.  在“分区管理器”中，作为当前直接查询分区的分区由分区名称上的前缀 **(DirectQuery)** 指示。****  
  
     从 **“分区”** 列表中选择一个不同的分区，然后单击 **“设置为 DirectQuery”**。 在选择当前 DirectQuery 分区时 **“设置为 DirectQuery”** 按钮未启用，并且在尚未为直接查询模式启用模型时不可见。  
  
4.  如果需要，请更改处理选项，然后单击 **“确定”**。  
  
### <a name="change-the-directquery-partition-for-a-deployed-tabular-model"></a>更改已部署表格模型的 DirectQuery 分区  
  
1.  在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]的对象资源管理器中，打开模型数据库。  
  
2.  展开“表”节点，右键单击已分区表，然后选择“分区”。********  
  
     为用于 DirectQuery 模式而指定的分区在分区名称上具有前缀 (DirectQuery)。  
  
3.  若要更改为其他分区，请单击 **“直接查询”** 工具栏图标以便打开 **“设置 DirectQuery 分区”** 对话框。 在尚未为直接查询启用的模型上，DirectQuery 工具栏图标不可用。  
  
4.  从 **“分区名称”** 下拉列表中选择一个不同的分区，然后根据需要更改该分区上的处理选项。  
  
## <a name="see-also"></a>另请参阅  
 [分区（SSAS 表格）](tabular-models/partitions-ssas-tabular.md)  
  
  
