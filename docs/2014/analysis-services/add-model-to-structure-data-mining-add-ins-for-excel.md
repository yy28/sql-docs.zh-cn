---
title: 向结构中添加模型（Excel 数据挖掘外接程序） |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, creating
ms.assetid: 8efd5bf4-4e6a-4ee8-971a-6efaed5f3b76
author: minewiskan
ms.author: owend
ms.openlocfilehash: 606d453235529fbfed4dc0f07178ce2ae7132067
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2020
ms.locfileid: "84528253"
---
# <a name="add-model-to-structure-data-mining-add-ins-for-excel"></a>将模型添加到结构（Excel 数据挖掘外接程序）
  ![“将模型添加到结构”按钮](media/dmc-addmodel.gif "“将模型添加到结构”按钮")  
  
 单击 "**将模型添加到结构**" 时，将启动一个向导，该向导将帮助您创建新的挖掘模型以用于现有挖掘结构。 此选项十分有用，因为通过它可以比较基于相同数据的模型或创建自定义模型。  
  
 如果 Analysis Services 的实例尚未包含所需的数据，请使用 "[创建挖掘结构" &#40;SQL Server 数据挖掘外接程序 "&#41;](create-mining-structure-sql-server-data-mining-add-ins.md)向导来设置挖掘结构。 或者，可以启动一个建模向导，然后向该向导创建的结构添加新模型。  
  
 若要使用向导不支持的算法创建高级模型，请使用 "**数据挖掘高级查询编辑器**" 创建一个挖掘结构，然后添加一个模型。  
  
## <a name="add-a-new-model-to-an-existing-structure"></a>向现有结构添加新模型  
  
1.  在 "**数据挖掘**" 功能区上，单击 "**高级**" 下的箭头，然后选择 "**将模型添加到结构**"。  
  
2.  在 "**选择结构**" 对话框中，选择包含要使用的数据的结构，然后单击 "**下一步**"。  
  
     **提示**：如果你不确定哪个挖掘结构包含所需的数据，请使用**文档模型**向导查看有关数据的列和基本统计信息。  
  
     如果找不到挖掘结构，请检查当前使用的连接。 可能需要打开另一个服务器的连接。  
  
3.  在 "**选择挖掘算法**" 对话框中，选择要在新挖掘模型中使用的挖掘算法。  
  
     请注意，此对话框提供的选项比在向导中看到的选项多。 只要数据兼容，便可以使用 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 服务器上支持的任何算法创建模型。  
  
4.  建议您还可以单击 "**参数**" 按钮打开 "**算法参数**" 对话框并自定义算法的参数。 此选项是创建自定义挖掘模型的最简便方法。  
  
5.  单击“下一步”。  
  
6.  在 "**选择列**" 对话框中，查看列的列表，如有必要，请将列的用法更改为以下值之一：  
  
    -   输入。 指示列包含可能影响结果并且应用作模型输入的变量。  
  
    -   **输入和预测**。 指示数据应用作输入，并且您还要预测这些值。  
  
    -   **仅预测**。 指示数据不应用作模型的输入。  
  
    -   **Key**。 每个模型至少需要一个密钥。 根据模型类型，您还可以选择其他特殊键，如**SequenceKey**或**TimeKey**。  
  
    -   **请勿使用**。 指示数据不应在模型中使用（即使在结构中存在）。  
  
7.  单击浏览 **（...）** 按钮以打开 "**设置列模型标志**" 对话框。  
  
     花点时间验证每个数据列的用法是否适合于模型。 这是防止在尝试处理模型时发生错误的重要步骤。  
  
     例如，如果您重复使用为决策树模型创建的结构并对其应用 Naïve Bayes 算法，则具有数据类型 `Numeric` 和内容类型 `Continuous` 的列需要装箱或更改为离散变量。  
  
     如果结构中的列不适用于新算法，则可以通过选择 "不**使用**" 来跳过这些列。  
  
8.  在 "**设置列模型标志**" 对话框中，查看或设置建模标志（如果有）。  
  
     通过建模标志可以控制处理 null 的方式（但不仅限于此）。 有关详细信息，请参阅[建模标志（数据挖掘）](data-mining/modeling-flags-data-mining.md)。  
  
     完成后，单击 **"确定"** 关闭对话框。  
  
9. 在 "**完成**" 对话框中，键入新挖掘模型的名称和说明。  
  
     根据生成的模型类型，您还有以下选项：  
  
    -   生成之后浏览已完成的挖掘模型。  
  
    -   从模型对数据源使用钻取。  
  
         有关详细信息，请参阅[挖掘模型钻取](data-mining/drillthrough-on-mining-models.md)。  
  
10. 单击“完成”**** 以保存所做的更改。 执行此操作时，新模型会部署到服务器并进行处理。  
  
### <a name="related-options"></a>相关选项  
  
|选项|注释|  
|------------|--------------|  
|"**选择结构或模型**" 对话框|选择一种现有挖掘结构作为生成新模型的基础。  选取的结构必须位于当前连接上。 如果不是，则使用 "[连接到源数据" &#40;Excel&#41;工具的数据挖掘客户端来](connect-to-source-data-data-mining-client-for-excel.md)更改连接。|  
|"**选择挖掘算法**" 对话框|数据挖掘算法列表的内容取决于所连接的服务器。 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 在 Standard 和 Enterprise 版本中提供不同的算法。 管理员还可能添加了自定义算法。<br /><br /> 如果看不到任何算法，请验证是否已连接到的实例 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 。|  
|**算法参数**对话框|在这些设置中，可以使用特定于分析方法的参数自定义每个算法。 还可以设置种子以确保模型的结果可以在多个定型过程间重新生成。<br /><br /> 有关详细信息，请参阅[&#40;SQL Server 数据挖掘外接程序&#41;的算法参数](algorithm-parameters-sql-server-data-mining-add-ins.md)。|  
|**设置列模型标志**对话框|建模标志可通过指定缺失数据的处理方式来改进模型。 有关详细信息，请参阅[建模标志（数据挖掘）](data-mining/modeling-flags-data-mining.md)。|  
  
###  <a name="setting-column-usage"></a><a name="Bkmk_mdlcolumn"></a>设置列用法  
 向现有挖掘结构添加新的模型时，必须指定该模型将如何使用挖掘结构中的每个数据列。 您可能会发现，此向导中的选项比挖掘结构上的选项更详细。 为什么？  
  
 原因在于，使用向导一起创建模型和结构时，许多控制算法对数据的使用方式的选项会自动设置。 但是，向现有模型添加新模型时，需要手动查看这些选项，并指定数据是否应用于分析、数据类型是否正确等。  
  
 向现有数据应用新算法时您可能会收到错误消息，但是这些消息通常提供有关为允许处理模型而需要进行的更正的详细信息。 典型问题如下：  
  
-   模型需要的数据类型与结构包含的数据类型不同。  
  
     某些算法只能用于数字；某些算法只能用于文本。 如果数据对于新模型是错误类型，则可能需要修改结构以使模型可以进行处理。  
  
-   挖掘结构不包含任何可预测属性。  
  
     聚类分析模型在生成时可以不使用可预测值，但是其他模型通常需指定单个列用于预测。  
  
-   数据的构成与您选择的算法不兼容。  
  
     某些类型的分析需要根据唯一规则仔细构造的数据。 示例包括预测模型和关联模型。 可以方便地添加具有相同类型的新模型（可能包含自定义项），但是数据可能不适用于其他算法。  
  
### <a name="requirements"></a>要求  
 若要创建数据挖掘模型，必须具有到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例的连接。 有关如何创建或更改连接的详细信息，请参阅[连接到源数据 &#40;Excel 数据挖掘客户端&#41;](connect-to-source-data-data-mining-client-for-excel.md)。  
  
 如果看不到所需的数据挖掘结构，则可能是因为该结构已被保存到其他实例或 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库中。 有关如何更改为其他数据挖掘连接的信息，请参阅[连接到数据挖掘服务器](connect-to-a-data-mining-server.md)。  
  
## <a name="see-also"></a>另请参阅  
 [创建数据挖掘模型](creating-a-data-mining-model.md)   
