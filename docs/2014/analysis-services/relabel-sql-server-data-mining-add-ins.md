---
title: 重新标记 （SQL Server 数据挖掘外接程序） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data preparation
- relabel
- data cleaning
ms.assetid: af041b39-fdd1-4cb5-a5ef-2f3ddab84614
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5471720cbd3084c661dec93d9c7f4f680e066b86
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66070394"
---
# <a name="relabel-sql-server-data-mining-add-ins"></a>重新标记（SQL Server 数据挖掘外接程序）
  ![重新标记工具的 office 13 图标](media/dm13-relabel.gif "重新标记工具的 Office 13 图标")  
  
 使用 Excel 数据挖掘客户端可以为数据创建新标签，以便使分析结果更容易理解。  
  
 重新标记的原因包括：  
  
-   数据的结果经过编码，如 1 表示男性，2 表示女性。  
  
-   要将数值装入存储桶，并希望为范围给出一个说明性名称。  
  
-   要简化长名称。  
  
## <a name="using-the-relabel-wizard"></a>使用重新标记向导  
  
1.  在中**数据挖掘**功能区中，单击**清理**，然后选择**重新标记**。  
  
2.  选择具有要修复的数据的表或数据范围。  
  
3.  在中**重新标记**页的向导中，选择一个列中，通过从下拉列表中选择列或通过单击中的列**数据示例**窗格。  
  
     **数据示例**窗格只显示大约 50 行数据，但若要确保你看到了好的值分布进行采样。  
  
     单击列标题**计数**要作为排序依据每个值的计数。  
  
     您还可以按排序**原始标签**，这会很方便，如果你想要首先重新标记所有最高或最低值。  
  
4.  在中**重新标记**数据页的向导中，查看中的值**原始标签**列，并决定你想要进行分组或对其进行编辑。  
  
5.  下方的行中键入新值**新标签**。 您还可以从现有值列表中选择值。 随着您键入新值，这些值将立即可供重复使用。  
  
6.  输入足够的行后，单击**下一步**，然后在**选择目标**页上，选择将在其中保存重新标记的数据。  
  
    -   **将作为新列添加到当前工作表**  
  
         单击此选项可将包含新值的新列添加到表中。  
  
    -   **将工作表数据及其更改复制到新的工作表**  
  
         单击此选项可创建一个包含更新数据的新工作表。  
  
    -   **就地更改数据**  
  
         单击此选项可将原始数据替换为新值。  
  
## <a name="see-also"></a>请参阅  
 [浏览和清除数据](exploring-and-cleaning-data.md)  
  
  
