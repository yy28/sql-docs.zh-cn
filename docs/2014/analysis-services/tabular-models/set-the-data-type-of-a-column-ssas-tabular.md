---
title: 设置列 (SSAS 表格) 的数据类型 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 34e2d508-7b64-4503-a4f0-c6c6ad5f8a44
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 82b2d4a687c490ed1909a27fc55fdece9cc3662c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48083207"
---
# <a name="set-the-data-type-of-a-column-ssas-tabular"></a>设置列的数据类型（SSAS 表格）
  导入数据或将数据粘贴到模型时，模型设计器将自动检测并应用数据类型。 在将数据添加到模型后，您可以手动修改列的数据类型以便更改数据的存储方式。 如果只想更改显示数据的格式而不更改其存储方式，可以采用其他方法。  
  
### <a name="to-change-the-data-type-or-display-format-for-a-column"></a>更改列的数据类型或显示格式  
  
1.  在模型设计器中，选择要更改数据类型或显示格式的列。  
  
2.  在列 **“属性”** 窗口中，执行以下操作之一：  
  
    -   在 **“数据格式”** 属性中，选择一个不同的数据格式。  
  
    -   在 **“数据类型”** 属性中，选择一个不同的数据类型。  
  
## <a name="considerations-when-changing-data-types"></a>更改数据类型时的注意事项  
 有时您尝试更改列的数据类型或选择数据转换时，可能出现以下错误之一：  
  
-   无法更改数据类型  
  
-   无法更改列数据类型  
  
 即使数据类型是“数据类型”下拉列表中的可用选项，也可能出现这些错误。 本节说明这些错误的原因以及解决方法。  
  
### <a name="understanding-automatically-determined-data-types"></a>了解自动确定的数据类型  
 将数据添加到模型时，模型设计器检查数据列以查看每个列包含什么数据类型。 如果列中的数据是一致的，则将最精确的数据类型分配给该列。  
  
 但是，如果从 Excel 或不在每一列中强制使用单一数据类型的其他源添加数据，模型设计器将分配可容纳该列中所有值的数据类型。 因此，如果列包含不同类型的数字（如整数、长型数字和货币），模型设计器将使用小数数据类型。 如果列包含数字和文本，模型设计器将使用文本数据类型。 模型设计器不提供与 Excel 中的“常规”数据类型类似的数据类型。  
  
 因此，如果列同时包含数字和文本值，将无法将该列转换为数值数据类型。  
  
 下列数据类型在商业智能语义模型中可用：  
  
|模型数据类型|  
|----------------------|  
|Text<br /><br /> 小数<br /><br /> 整数<br /><br /> 货币<br /><br /> TRUE/FALSE<br /><br /> date|  
  
 如果发现数据的数据类型错误或至少与期望的数据类型不同，可以选择以下处理方法：  
  
-   可以重新导入数据。 为此，请打开到数据源的现有连接并重新导入列。 根据数据源类型，您可能能够在导入过程中应用筛选器来删除问题值。  
  
-   可以在计算列中创建一个 DAX 公式，以创建所需数据类型的新值。 例如，可以使用 TRUNC 函数将小数更改为整数，或结合使用信息函数和逻辑函数来测试和转换值。  
  
### <a name="understanding-data-conversion"></a>了解数据转换  
 如果在选择数据转换选项时遇到错误，可能是因为列的当前数据类型不支持所选的转换。 并非所有转换都适用于所有数据类型。 例如，如果列的当前数据类型是数字（整数或小数）或文本，则只能将该列更改为布尔数据类型。 因此，您必须为列中的数据选择适当的数据类型。  
  
 选择适当的数据类型后，模型设计器将警告您可能对数据进行的更改，如降低精度或截断。 单击“确定”以接受并将您的数据更改为新数据类型。  
  
 如果支持该数据类型，但是模型设计器在新数据类型中发现不支持的值，将遇到另一个错误，在继续操作前您需要更正数据值。  
  
 有关使用商业智能语义模型中的数据类型的详细信息，它们是隐式转换后，以及如何将不同数据类型的方式是在公式中使用，请参阅[支持的数据类型&#40;SSAS 表格&#41;](data-types-supported-ssas-tabular.md).  
  
## <a name="see-also"></a>请参阅  
 [支持的数据类型&#40;SSAS 表格&#41;](data-types-supported-ssas-tabular.md)  
  
  
