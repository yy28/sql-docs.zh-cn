---
title: 键列对话框 (Analysis Services-多维数据) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql.asvs.dimensiondesigner.dbv.dataitemCollection.f1
helpviewer_keywords:
- DataItem Collection dialog box
ms.assetid: 585f27f2-d5eb-4516-b29a-2084010b7d51
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6c67966895699c34d58a0527ea27c06e7cc05ed5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48049047"
---
# <a name="key-columns-dialog-box-analysis-services---multidimensional-data"></a>“键列”对话框（Analysis Services - 多维数据）
  可以使用 **“键列”** 对话框更改特性的 **KeyColumns** 属性。 有关详细信息，请参阅 [修改特性的 KeyColumn 属性](multidimensional-models/attribute-properties-modify-the-keycolumn-property.md)。  
  
 **若要显示键列对话框**  
  
-   在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中，选择一个特性，然后在“属性”窗口中单击与该特性的 **KeyColumns** 属性关联的省略号按钮 (**...**)。  
  
## <a name="options"></a>选项  
 **源表**  
 选择要选择其键列的源表。 可以从数据源视图的所有表列表中选择源表。  
  
 **可用列**  
 选择要用作键列的列。 可以从指定的 **“源表”** 的列列表中选择尚未选为键列的列。  
  
 若要添加到所选的列**键列**列表中，单击**>** 按钮。  
  
 **键列**  
 定义所选键列的顺序。 键列的顺序对于定义正确的组合键非常重要。 若要排序或重新排序键列列表，请选择列，然后单击 **“向上”** 或 **“向下”** 按钮。  
  
 若要从“键列”列表中删除列，请选择列，然后单击 **“键列”** 按钮 **\<** 。  
  
 **向上**  
 单击此项可在“键列”中将所选列上移一个位置。  
  
> [!NOTE]  
>  仅当列表中包含一个以上列并且选定某列时，才启用此选项。  
  
 **向下**  
 单击此项可在“键列”中将所选列下移一个位置。  
  
> [!NOTE]  
>  仅当列表中包含一个以上列并且选定某列时，才启用此选项。  
  
 **>**  
 单击此项可将新列添加到“键列”中列出的列的末尾。  
  
 **<**  
 单击此项可将所选列从“键列”中列出的列中删除。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 设计器和对话框&#40;多维数据&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)  
  
  
