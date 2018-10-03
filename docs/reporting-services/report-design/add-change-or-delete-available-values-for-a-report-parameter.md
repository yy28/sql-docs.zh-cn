---
title: 为报表参数添加、更改或删除可用值 | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
f1_keywords:
- sql13.rtp.rptdesigner.reportparameters.availablevalues.f1
- "10455"
- "10071"
ms.assetid: 0e03264c-523f-4c59-b71b-ceef600f75f6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: f1efe1e5e10905cb04b2449ba0497af2b43f7aef
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47804195"
---
# <a name="add-change-or-delete-available-values-for-a-report-parameter"></a>为报表参数添加、更改或删除可用值
  创建报表参数后，可以指定向用户显示的可用值列表。 可用值列表将限制用户只能选择参数的有效值。  
  
 报表运行时，可用值会显示在工具栏中报表参数旁的下拉列表中。 报表参数可以是单值参数或多值参数。 对于多值参数，列表的顶部具有一个 **“全选”** 功能，因此用户只需一次单击即可选中或取消选中所有值。  
  
 您可以提供静态值列表或来自报表数据集的值列表。 还可以通过指定标签字段为这些值提供友好名称。 例如，对于基于 `ProductID` 字段的参数，可以在参数标签中显示 `ProductName` 字段。 报表运行时，用户可以从产品名称中进行选择，但是实际选定的值为相应的 `ProductID`。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 在您发布某一报表后，您可以通过对报表服务器设置参数属性值，在报表创作工具中覆盖在报表中定义的可用值。 有关详细信息，请参阅 [报表参数（报表生成器和报表设计器）](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)的详细信息。  
  
### <a name="to-add-or-change-the-available-values-for-a-report-parameter"></a>添加或更改报表参数的可用值  
  
1.  在“报表数据”窗格中，展开“参数”节点。 右键单击该参数，然后单击“参数属性”。 此时将打开 **“报表参数属性”** 对话框。  
  
    > [!NOTE]  
    >  如果“报表数据”窗格不可见，请单击“视图”，然后单击“报表数据”。  
  
2.  单击 **“可用值”**。 选择可用值选项：  
  
    -   单击“指定值”可手动提供值列表，还可以为值提供友好名称（标签）。  
  
         单击 **“添加”** ，然后在 **“值”** 文本框中输入值，或在 **“标签”** 文本框中输入标签。 如果不提供标签，将使用输入的值。 您可以为值编写表达式。 数据类型必须与参数的数据类型相匹配。 字段名称不能用于参数的表达式中。 有关示例，请参阅[常用筛选器（报表生成器和 SSRS）](../../reporting-services/report-design/commonly-used-filters-report-builder-and-ssrs.md)。  
  
         为要提供的每个值重复此步骤。 您在此列表中看到的项的顺序将决定用户在下拉列表中看到这些项的顺序。 若要更改列表中某一项的顺序，请单击 **“值”** 或 **“标签”** 文本框选择该项，然后使用向上箭头或向下箭头按钮在列表中上下移动该项。  
  
    -   单击 **“从查询中获取值”** 可提供检索此参数的值或友好名称的现有数据集的名称。  
  
        > [!IMPORTANT]  
        >  如果相同数据集包含该报表参数的对应查询参数，则该报表会在您尝试运行它时显示错误消息。 您可使用不同的数据集检索值，从而解决此错误。  
  
         在 **“数据集”** 中，选择该数据集的名称。  
  
         在 **“值字段”** 中，选择提供参数值的字段的名称。  
  
         在 **“标签字段”** 中，选择提供参数友好名称的字段的名称。 如果友好名称没有单独的字段，则为其选择与 **“值”** 字段相同的字段。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     预览该报表时，将看到参数的可用值下拉列表。  
  
### <a name="to-remove-the-available-values-for-a-report-parameter"></a>删除报表参数的可用值  
  
1.  在“报表数据”窗格中，展开“参数”节点。 右键单击该参数，然后单击“参数属性”。 将打开 **“Report Parameters”** 对话框。  
  
2.  单击 **“可用值”**。  
  
3.  在 **“选择以下选项之一”** 中，单击 **“无”**。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     预览该报表时，将不再显示参数的可用值下拉列表。  
  
## <a name="see-also"></a>另请参阅  
 [更改报表参数的顺序（报表生成器和 SSRS）](../../reporting-services/report-design/change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)   
 [添加、更改或删除报表参数（报表生成器和 SSRS）](../../reporting-services/report-design/add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md)   
 [向报表添加级联参数（报表生成器和 SSRS）](../../reporting-services/report-design/add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)   
 [为报表参数添加、更改或删除默认值（报表生成器和 SSRS）](../../reporting-services/report-design/add-change-or-delete-default-values-for-a-report-parameter.md)   
 [参数集合引用（报表生成器和 SSRS）](../../reporting-services/report-design/built-in-collections-parameters-collection-references-report-builder.md)   
 [教程：向报表添加参数（报表生成器）](../../reporting-services/tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [表达式（报表生成器和 SSRS）](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  
