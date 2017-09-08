---
title: "复制和粘贴数据 (SSAS 表格) |Microsoft 文档"
ms.custom: 
ms.date: 05/22/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.bidtoolset.pastepreviewdb.f1
ms.assetid: 2f8d8b3d-810b-4c31-98f2-341015e13da8
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5bbc30ea67df15827da8b289fe1481beee0b6016
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="import-data---copy-and-paste-data"></a>导入数据的复制和粘贴数据
  可以从外部应用程序复制表数据并将它粘贴到模型设计器中的新表或现有表。 从剪贴板粘贴的数据必须是 HTML 格式，例如，从 Excel 或 Word 中复制的数据。 模型设计器将对粘贴数据自动检测并应用数据类型。 您也可以手动修改列的数据类型或显示格式。  
  
 与具有数据源连接的表不同，粘贴的表没有“连接名称”或“源数据”属性。 粘贴的数据在 Model.bim 文件中保持不变。 保存项目或 Model.bim 文件时，也保存粘贴的数据。  
  
 部署模型时，无论在部署时是否处理模型，都还将部署粘贴的数据。  
  
 本主题的内容：  
  
-   [先决条件](#bkmk_prerequisites)  
  
-   [粘贴数据](#bkmk_paste_data)  
  
-   [“粘贴预览”对话框](#bkmk_paste_preview)  
  
##  <a name="bkmk_prerequisites"></a> 先决条件  
 粘贴数据时存在一些限制：  
  
-   粘贴的表的行数不能超过 10,000。  
  
-   粘贴的表不能分区。  
  
-   在 DirectQuery 模式中不支持粘贴的表。  
  
-   仅当使用通过从剪贴板粘贴数据初始创建的表时， **“追加粘贴”** 和 **“替换粘贴”** 选项才可用。 不能使用 **“追加粘贴”** 或 **“替换粘贴”** 向导入的数据来自另一数据源类型的表添加数据。  
  
-   当使用 **“追加粘贴”** 或 **“替换粘贴”**时，新数据必须与原始数据包含相同列数。 最好是粘贴或追加的数据列还应与目标表中的那些数据列属于相同的数据类型或兼容的数据类型。 在某些情况下，可以使用不同的数据类型，但可能会显示“类型不匹配”  错误。  
  
##  <a name="bkmk_paste_data"></a> 粘贴数据  
  
#### <a name="to-paste-data-into-the-designer"></a>向设计器粘贴数据  
  
-   在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，单击 **“编辑”** 菜单，然后单击以下项之一：  
  
    -   单击 **“粘贴”** 可以将剪贴板的内容粘贴到新表中。  
  
    -   单击 **“追加粘贴”** 可以将剪贴板内容作为附加行粘贴到所选表中。 新行将添加到表的末尾。  
  
    -   单击 **“替换粘贴”** 可以用剪贴板内容取代所选表。 所有现有列标题的名称都将保留在表中，并且将保留关系。  
  
##  <a name="bkmk_paste_preview"></a> “粘贴预览”对话框  
 **“粘贴预览”** 对话框可用于查看复制到设计器窗口中的数据的预览以及确保数据正确复制。 若要访问此对话框，请将 HTML 格式的基于表的数据复制到剪贴板中，然后在设计器中，单击“编辑”菜单，然后单击“粘贴”、“追加粘贴”或“替换粘贴”。 仅当通过从剪贴板复制和粘贴来添加或替换所创建的表中的数据时， **“粘贴追加”** 和 **“粘贴替换”** 选项才可用。 不能使用 **“粘贴追加”** 或 **“粘贴替换”** 向包含导入数据的表添加数据。  
  
 根据您是将数据粘贴到全新的表中，将数据粘贴到现有表中并用新数据替换现有数据，还是将数据追加到现有表中，此对话框的选项将有所不同。  
  
### <a name="paste-to-new-table"></a>粘贴到新表中  
 **表名**  
 指定将在设计器窗口中创建的表的名称。  
  
 **要粘贴的数据**  
 显示将添加到目标表中的剪贴板内容的示例。  
  
### <a name="paste-append"></a>“追加粘贴”  
 **表中的现有数据**  
 显示表中现有数据的示例，以便您可以验证列、数据类型等等。  
  
 **要粘贴的数据**  
 显示剪贴板内容的示例。 将为现有数据追加此数据。  
  
### <a name="paste-replace"></a>“替换粘贴”  
 **表中的现有数据**  
 显示表中现有数据的示例，以便您可以验证列、数据类型等等。  
  
 **要粘贴的数据**  
 显示剪贴板内容的示例。 目标表中的现有数据将被删除，并且将新行插入到表中。  
  
## <a name="see-also"></a>另请参阅  
 [导入数据（SSAS 表格）](http://msdn.microsoft.com/library/6617b2a2-9f69-433e-89e0-4c5dc92982cf)   
 [支持的数据源（SSAS 表格）](../../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md)   
 [设置列的数据类型（SSAS 表格）](../../analysis-services/tabular-models/set-the-data-type-of-a-column-ssas-tabular.md)  
  
  
