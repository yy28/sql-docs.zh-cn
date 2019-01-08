---
title: 将表添加到 Analysis Services 表格模型 |Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 224df75c15acf560c7eadc70fe91fbbc2b0396d9
ms.sourcegitcommit: 8a64c59c5d84150659a015e54f8937673cab87a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2018
ms.locfileid: "53072284"
---
# <a name="add-a-table"></a>添加表
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  本文介绍如何从数据源从其以前的数据导入您的模型中添加表。 若要添加来自同一数据源的表，您可以使用现有的数据源连接。 建议您在从单个数据源导入任意数量的表时始终使用单个连接。  
  
### <a name="to-add-a-table-from-an-existing-data-source"></a>从现有数据源添加表  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，单击 **“模型”** 菜单，然后单击 **“现有连接”**。  
  
2.  在 **“现有连接”** 页中，选择指向要添加的表所在的数据源的连接，然后单击 **“打开”**。  
  
3.  在 **“选择表和视图”** 页上，从数据源中选择要添加到模型中的表。  
  
    > [!NOTE]  
    >  **“选择表和视图”** 页不会将以前导入的表显示为已选中。  如果使用此连接选择以前曾导入的表，且以前未曾为该表指定不同的友好名称，则将向该友好名称追加一个数字 1。 无需重新选择以前使用此连接导入的任何表。  
  
4.  如有必要，请使用“预览和筛选”以便仅选择特定列或对要导入的数据应用筛选器。  
  
5.  单击 **“完成”** 导入新表。  
  
> [!NOTE]  
>  从单个数据源同时导入多个表时，这些表在数据源中所具备的任何表间关系都将在模型中自动创建。 但如果稍后添加表，则可能需要在模型中手动创建新添加的表和以前导入的表之间的关系。  
  
## <a name="see-also"></a>另请参阅  
 [导入数据](http://msdn.microsoft.com/library/6617b2a2-9f69-433e-89e0-4c5dc92982cf)   
 [删除表](../../analysis-services/tabular-models/delete-a-table-ssas-tabular.md)  
  
  
