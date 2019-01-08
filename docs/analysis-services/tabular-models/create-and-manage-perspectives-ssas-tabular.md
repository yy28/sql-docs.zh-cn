---
title: 创建和管理 Analysis Services 表格模型中的透视 |Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 962b6b90de6d95107d1a4cdd3484a44205afb630
ms.sourcegitcommit: 8a64c59c5d84150659a015e54f8937673cab87a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2018
ms.locfileid: "53071844"
---
# <a name="create-and-manage-perspectives"></a>创建和管理透视 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  透视定义某一模型的可查看子集，借此您可以将注意力集中在该模型中的特定业务或特定应用上。 本主题中的任务说明如何使用模型设计器中的 **“透视”** 对话框来创建和管理透视。  
  
## <a name="tasks"></a>“任务”  
 为了创建透视，您将使用 **“透视”** 对话框，您可以在此添加、编辑、删除、复制和查看透视。 若要查看 **“透视”** 对话框，请在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中单击 **“模型”** 菜单，然后单击 **“透视”**。  
  
###  <a name="bkmk_add"></a> 添加透视  
  
-   若要添加新的透视，请单击 **“新建透视”**。 然后，您可以选中和取消选中要包括的字段对象，并为新的透视提供名称。  
  
     如果您创建具有所有字段对象字段的一个空透视，则使用该透视的用户将看到一个空的字段列表。 透视应包含至少一个表和列。  
  
###  <a name="bkmk_edit"></a> 编辑透视  
  
-   若要修改某一透视，选中或取消选中透视的列，这将添加从透视中删除字段对象中的字段。  
  
###  <a name="bkmk_rename"></a> 重命名透视  
  
-   当鼠标悬停在透视的列标题 （透视的名称） 上**重命名**按钮将出现。 若要重命名该透视，请单击 **“重命名”**，然后输入新名称或编辑现有名称。  
  
###  <a name="bkmk_delete"></a> 删除透视  
  
-   当鼠标悬停在透视的列标题 （透视的名称） 上**删除**按钮将出现。 若要删除透视，请单击 **“删除”** 按钮，然后在确认窗口中单击 **“是”** 。  
  
###  <a name="bkmk_copy"></a> 复制透视  
  
-   当您将鼠标悬停在透视的列标题**复制**按钮将出现。 若要创建该透视的副本，请单击 **“复制”** 按钮。 所选透视的副本将作为新透视添加到现有透视的右侧。 新的透视将继承复制的透视的名称，并且“复制”批注将追加到名称的末尾。 例如，如果一份*销售*创建角度来看，新的透视将称作*Sales-Copy*。  
  
## <a name="see-also"></a>另请参阅  
 [透视](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)   
 [层次结构](../../analysis-services/tabular-models/hierarchies-ssas-tabular.md)  
  
  
