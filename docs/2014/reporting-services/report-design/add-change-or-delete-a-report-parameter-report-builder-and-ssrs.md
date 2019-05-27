---
title: 添加、更改或删除报表参数（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: d44a8e0a-10cf-4502-9391-09743ffc9bad
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ebf333b49c20c7eadef4fdbcd54834c450d274c6
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66106689"
---
# <a name="add-change-or-delete-a-report-parameter-report-builder-and-ssrs"></a>添加、更改或删除报表参数（报表生成器和 SSRS）
  报表参数为选择报表数据、连接相关报表以及更改报表显示提供了一种方法。 您可以提供一个默认值和一列可用值，用户可以更改所选值。  
  
 报表发布后，您可以在报表服务器上更改报表参数的默认值、可用值以及其他属性。 通过创建链接报表，您可以提供多组默认参数值。 有关详细信息，请参阅位于 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SQL Server 联机丛书 [上的](https://go.microsoft.com/fwlink/?linkid=120955)文档中的“设置已发布报表的参数属性”。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-or-edit-a-report-parameter"></a>添加或编辑报表参数  
  
1.  在 **“报表数据”** 窗格中，右键单击 **“参数”** 节点，然后单击 **“添加参数”**。 此时将打开 **“报表参数属性”** 对话框。  
  
2.  在 **“名称”** 中，键入参数的名称，或接受默认名称。  
  
3.  在 **“提示”** 中，键入当用户运行报表时，参数文本框旁边将会显示的文本。  
  
4.  在 **“数据类型”** 中，选择参数值的数据类型。  
  
5.  如果参数可以包含空白值，请选择 **“允许空白值”**。  
  
6.  如果参数可以包含 Null 值，请选择 **“允许 Null 值”**。  
  
7.  若要允许用户为参数选择多个值，请选择 **“允许多个值”**。  
  
8.  设置可见性选项。  
  
    -   若要在报表顶部的工具栏中显示参数，请选择 **“可见”**。  
  
    -   若要隐藏参数使其不显示在工具栏中，请选择 **“隐藏”**。  
  
    -   若要隐藏参数，以保护其不会在报表发布后，被从报表服务器上修改，请选择 **“内部”**。 这样将仅可在报表定义中查看该报表参数。 对于此选项，您必须设置一个默认值，或允许参数接受 Null 值。  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-delete-a-report-parameter"></a>删除报表参数  
  
1.  在 **“报表数据”** 窗格中，展开 **“参数”** 节点。  
  
2.  右键单击报表参数，然后单击 **“删除”**。  
  
## <a name="see-also"></a>请参阅  
 [为报表参数添加、更改或删除可用值（报表生成器和 SSRS）](add-change-or-delete-available-values-for-a-report-parameter.md)   
 [为报表参数添加、更改或删除默认值（报表生成器和 SSRS）](add-change-or-delete-default-values-for-a-report-parameter.md)   
 [更改报表参数的顺序（报表生成器和 SSRS）](change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)   
 [报表参数（报表生成器和报表设计器）](report-parameters-report-builder-and-report-designer.md)   
 [用于对话框、窗格和向导的报表生成器帮助](../report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [向报表添加级联参数（报表生成器和 SSRS）](add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)   
 [教程：向报表添加参数（报表生成器）](../tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [教程&#40;报表生成器&#41;](../report-builder-tutorials.md)   
 [添加数据集筛选器、数据区域筛选器和组筛选器（报表生成器和 SSRS）](add-dataset-filters-data-region-filters-and-group-filters.md)   
 [参数集合引用（报表生成器和 SSRS）](built-in-collections-parameters-collection-references-report-builder.md)   
 [将多值参数添加到报表](add-a-multi-value-parameter-to-a-report.md)  
  
  
