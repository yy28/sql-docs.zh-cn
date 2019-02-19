---
title: 创建递阶报表（报表生成器和 SSRS）| Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 5933c4f0-c713-4ecb-b521-ff46c9c63fff
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 8176db14311914a3935d86fdf83cc88e5428630f
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2019
ms.locfileid: "56295570"
---
# <a name="create-a-stepped-report-report-builder-and-ssrs"></a>创建递阶报表（报表生成器和 SSRS）
递阶报表是一种  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 分页报表，可在父组下方的同一列中缩进显示详细信息行或子组，如下例所示：  
  
 ![呈现的递阶报表](../../reporting-services/report-design/media/steppedreportrendered.gif "Rendered stepped report")  
  
 传统的表报表将父组放置在报表中的相邻列中。 利用新的 tablix 数据区域，可以向同一列添加组和详细信息行或子组。 若要将组行与详细信息行或子组行区分开来，可以应用格式设置（如字体颜色）或缩进详细信息行。  
  
 本主题中的过程说明如何手动创建递阶报表，但您也可以使用新建表和矩阵向导。 该向导为递阶报表提供布局，以便于创建递阶报表。 在完成该向导后，您可以进一步增强该报表。  
  
> [!NOTE]  
>  向导仅在报表生成器中可用。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-create-a-stepped-report"></a>创建递阶报表  
  
1.  创建一个表报表。 例如，插入一个 tablix 数据区域，然后向数据行中添加字段。  
  
2.  向报表添加一个父组。  
  
    1.  单击表中的任意位置以选择该表。 “分组”窗格将显示“行组”窗格中的详细信息组。  
  
    2.  在“分组”窗格中，右键单击“详细信息”组，指向“添加组”，然后单击“父组”。  
  
    3.  在“Tablix 组”对话框中，为该组提供一个名称，并键入或从下拉列表中选择组表达式。 该下拉列表显示了“报表数据”窗格中可用的简单字段表达式。 例如，[PostalCode] 是数据集中 PostalCode 字段的简单字段表达式。  
  
    4.  选择 **“添加组头”**。 选择此选项将向组的上方添加一个组标签和组合计的静态行。 同样地，可以选择 **“添加组尾”** 在组的下方添加一个静态行。 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     现在即创建了一个基本表格报表。 此报表呈现时，您将看到一列组实例值，以及一列或多列分组的详细信息数据。 下图显示了该数据区域在设计图面上可能的外观。  
  
     ![带有组的表数据区域](../../reporting-services/report-design/media/tabledataregionwithgroup.gif "Table data region with group")  
  
     下图显示了您查看报表时所呈现的数据区域可能的外观。  
  
     ![呈现的分组报表](../../reporting-services/report-design/media/tablereportrendered.gif "Rendered grouped report")  
  
3.  对于递阶报表，不需要用于显示组实例的第一列。 相反，需要先复制组头单元中的值，再删除组列，然后将该值粘贴到组头行的第一个文本框中。 若要删除组列，请右键单击相应的组列或单元，然后单击“删除列”。 下图显示了该数据区域在设计图面上可能的外观。  
  
     ![带有组头行的数据区域](../../reporting-services/report-design/media/tabledataregiongroupheader.gif "Data region with group header row")  
  
4.  若要使同一列中组头行下方的详细信息行缩进显示，请更改详细信息数据单元的空白大小。  
  
    1.  选择包含要缩进显示的详细信息字段的单元。 该单元的文本框属性显示在“属性”窗格中。  
  
    2.  在“属性”窗格的 **“对齐”** 下，展开 **“填充”** 的属性。  
  
    3.  对于“左” ，键入一个新的填充值，例如 **.5in**。 填充会在单元中按照您指定的值缩进文本。 默认空白大小为 2 磅。 填充属性的有效值是零或正数，后跟一个大小指示符。  
  
         大小指示符有：  
  
        |||  
        |-|-|  
        |**in**|英寸（1 英寸 = 2.54 厘米）|  
        |**cm**|厘米|  
        |**mm**|毫米|  
        |**pt**|磅（1 磅 = 1/72 英寸）|  
        |**pc**|派卡（1 派卡 = 12 磅）|  
  
     数据区域的外观将与下例类似。  
  
     ![递阶报表的数据区域](../../reporting-services/report-design/media/steppedreportdataregion.gif "Data region for stepped report")  
  
     **递阶报表布局的数据区域**  
  
     在 **“主文件夹”** 选项卡上，单击 **“运行”**。 报表将根据子组值的缩进级别显示组。  
  
## <a name="to-create-a-stepped-report-with-multiple-groups"></a>创建包含多个组的递阶报表  
  
1.  按照前面步骤中所述创建一个报表。  
  
2.  向报表添加其他组。  
  
    1.  在“行组”窗格中，右键单击组，再单击“添加组”，然后选择要添加的组的类型。  
  
        > [!NOTE]  
        >  可以通过若干种方式向数据区域添加组。 有关详细信息，请参阅 [在数据区域中添加或删除组（报表生成器和 SSRS）](../../reporting-services/report-design/add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md)。  
  
    2.  在 **“Tablix 组”** 对话框中，键入一个名称。  
  
    3.  在 **“组表达式”** 中，键入一个表达式或选择要用作分组依据的数据集字段。 要创建表达式，请单击表达式 (fx) 按钮打开“表达式”对话框。  
  
    4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
3.  更改用于显示组数据的单元的填充值。  
  
## <a name="see-also"></a>另请参阅  
 [页眉和页脚（报表生成器和 SSRS）](../../reporting-services/report-design/page-headers-and-footers-report-builder-and-ssrs.md)   
 [设置报表项的格式（报表生成器和 SSRS）](../../reporting-services/report-design/formatting-report-items-report-builder-and-ssrs.md)   
 [Tablix 数据区域（报表生成器和 SSRS）](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)   
 [表（报表生成器和 SSRS）](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)   
 [矩阵（报表生成器和 SSRS）](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)   
 [列表（报表生成器和 SSRS）](../../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [表、矩阵和列表（报表生成器和 SSRS）](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
