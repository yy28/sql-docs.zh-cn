---
title: 处理数据疑难解答（SSAS 表格） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 678f523c-e181-4456-9a54-7b7bf044b8d2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f76d67d5e44fc700d4b889840ef2dcc07a0bfde0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66065768"
---
# <a name="troubleshoot-process-data-ssas-tabular"></a>数据处理故障排除（SSAS 表格）
  本主题提供有关在使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]创建模型时处理（刷新）模型数据的信息。 它不提供有关处理已部署到 Analysis Services 服务器实例的模型中的数据的信息。 有关处理已部署的模型中的数据的详细信息，请参阅 [在 Analysis Services 中编写管理任务脚本](script-administrative-tasks-in-analysis-services.md)。  
  
 本主题的内容：  
  
-   [数据处理的工作机制](#bkmk_how_df_works)  
  
-   [数据处理的影响](#bkmk_impact_of_df)  
  
-   [确定数据源](#bkmk_det_source)  
  
-   [确定最后刷新数据的时间](#bkmk_det_last_ref)  
  
-   [对可刷新数据源的限制](#bkmk_restrictions)  
  
-   [对数据源的更改限制](#bkmk_rest_changes)  
  
##  <a name="bkmk_how_df_works"></a>数据处理的工作原理  
 处理数据时，模型设计器中的数据将替换为新数据。 不能只导入新数据行或更改的数据。 模型设计器不跟踪之前添加了哪些行。  
  
 数据处理以事务形式执行。 这意味着一旦开始更新数据，整个更新不是失败就是成功；绝不会出现部分数据正确的情况。  
  
 从 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]启动的手动数据处理由 Analysis Services 的本地内存中实例来处理。 因此，数据处理操作会对计算机中其他任务的性能产生影响。 但是，如果你使用脚本在已部署的模型中安排数据的自动处理，该 Analysis Services 实例将管理导入过程及其时间。  
  
##  <a name="bkmk_impact_of_df"></a>数据处理的影响  
 数据的处理通常会触发数据的重新计算。  处理数据意味着从外部源获取最新数据；重新计算意味着更新使用已更改数据的所有公式的结果。 处理操作通常会触发重新计算。  
  
 因此，在更改数据源或处理从数据源中获取的数据之前，您应该始终注意潜在影响，还要考虑以下潜在后果：  
  
-   模型数据的某些部分可能由于数据源中的更改而被破坏。 如果并非所有列都可从数据源中进行检索（例如，如果这些列已被删除或更改），那么处理将失败，您必须更新源数据与模型数据之间的映射。 有关详细信息，请参阅 [编辑现有数据源连接（SSAS 表格）](edit-an-existing-data-source-connection-ssas-tabular.md)创建模型时处理（刷新）模型数据的信息。  
  
-   在处理后，某些列可能被标记为包含错误。 发生此情况的原因是：列中的 DAX 公式使用的数据在您进行处理时变得不可用、列的数据类型发生更改或向外部数据中添加了无效值。 若要解决此问题，您可以编辑该公式或删除该列（如果它基于不再可用的数据）。  
  
-   将需要重新计算使用更新的数据的公式。 根据模型的大小，这一重新计算可能花费一些时间。  
  
-   如果您的模型包含多个数据源，那么即使只有一个外部数据源发生了更改，您也可能需要处理整个模型（“全部处理”）。 例如，如果您创建依赖于计算列的度量值，并且这些计算列使用其他计算列中的值，则模型设计器将首先分析依赖关系，然后按顺序处理相关对象的整个链。 根据依赖关系的复杂程度，此操作可能会花费较长时间。  
  
-   更改筛选器时，必须重新计算整个模型。  
  
##  <a name="bkmk_det_source"></a>确定数据源  
 如果您不确定模型中数据的来源，可以使用 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] 中的工具获取详细信息，包括源文件的名称和路径。  
  
#### <a name="to-find-the-source-of-existing-data"></a>查找现有数据的源  
  
1.  在模型设计器中，选择包含要了解其源的数据的表。  
  
2.  单击 **“表”** 菜单，然后单击 **“表属性”**。  
  
3.  在 **“编辑表属性”** 对话框中，记下为 **“连接名称”** 列出的值。  
  
4.  在 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]的 **“模型”** 菜单上，单击 **“现有连接”**。  
  
5.  在 **“现有连接”** 对话框中，选择具有您在步骤 3 中找到的名称的数据源，然后单击 **“编辑”**。  
  
6.  在 **“编辑连接”** 对话框中查看连接信息，如数据库名称、文件路径或报表路径。  
  
##  <a name="bkmk_det_last_ref"></a>确定最后刷新数据的时间  
 可以使用“表属性”确定最后刷新数据的时间。  
  
#### <a name="to-find-the-date-and-time-that-a-table-was-last-processed"></a>查找最后处理表的日期和时间  
  
1.  在模型设计器中，选择包含要了解其刷新日期的数据的表。  
  
2.  单击 **“表”** 菜单，然后单击 **“表属性”**。  
  
3.  在 **“编辑表属性”** 对话框中， **“最后刷新时间”** 显示刷新表的最后日期。  
  
##  <a name="bkmk_restrictions"></a>对可刷新数据源的限制  
 对于可从 Analysis Services 实例上已部署的模型进行自动处理的数据源，存在一些限制。 请务必仅选择满足以下条件的那些数据源：  
  
-   该数据源必须在进行数据处理时可用，并且还必须在规定的位置上可用。 如果原始数据源处于创建此模型的用户的本地磁盘驱动器上，则必须或者从数据处理操作中排除该数据源，或者确定一种方法来将该数据源发布到可通过网络连接访问的位置。 如果您将某一数据源移到一个网络位置，请确保在模型设计器中打开模型并且重复数据检索步骤。 这是重新建立数据源连接属性中存储的连接信息所必需的。  
  
-   必须使用在数据源连接中嵌入的凭据来访问数据源。 当您连接到外部数据源时，在数据源连接中创建嵌入的凭据。  
  
-   数据处理必须对您指定的所有数据源均成功。 否则，处理的数据将被放弃，只会留下最后保存的模型版本。 因此，请排除您不确定的任何数据源。  
  
-   数据处理不得使模型中的其他数据失效。 在处理您的数据子集时，请务必了解在较新的数据与不是来自同一时间段的静态数据进行聚合后模型是否仍有效。 作为模型设计者，您要知道您的数据依赖关系并确保数据处理适合于模型本身。  
  
     外部数据源通过您在使用表导入向导将原始数据导入到模型时指定的嵌入连接字符串、URL 或 UNC 路径来访问。 在后续的数据刷新操作中将重用在数据源连接中存储的原始连接信息。 没有专为进行数据处理而创建和管理单独的连接信息；而只使用现有连接信息。  
  
##  <a name="bkmk_rest_changes"></a>对数据源的更改的限制  
 对于您可以对数据源进行的更改，存在一些限制：  
  
-   列的数据类型只能更改为兼容的数据类型。 例如，如果列中的数据中包含小数，则您无法将该数据类型更改为整数。 但是，您可以将数字数据更改为文本。 有关数据类型的详细信息，请参阅[支持的数据类型（SSAS 表格）](tabular-models/data-types-supported-ssas-tabular.md)。  
  
-   不能在不同表中多选列和更改列属性。 您一次只能使用一个表或视图。  
  
## <a name="see-also"></a>另请参阅  
 [手动处理 &#40;SSAS 表格&#41;的数据](manually-process-data-ssas-tabular.md)   
 [编辑现有数据源连接 &#40;SSAS 表格&#41;](edit-an-existing-data-source-connection-ssas-tabular.md)  
  
  
