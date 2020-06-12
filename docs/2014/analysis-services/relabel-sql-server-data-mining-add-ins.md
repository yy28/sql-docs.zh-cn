---
title: 重新标记（SQL Server 数据挖掘外接程序） |Microsoft Docs
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
ms.openlocfilehash: 7473f9c4dd9080fc03d3b1dea106f8b10c9c2916
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84539434"
---
# <a name="relabel-sql-server-data-mining-add-ins"></a>重新标记（SQL Server 数据挖掘外接程序）
  ![重新标记工具的 Office 13 图标](media/dm13-relabel.gif "重新标记工具的 Office 13 图标")

 使用 Excel 数据挖掘客户端可以为数据创建新标签，以便使分析结果更容易理解。

 重新标记的原因包括：

-   数据的结果经过编码，如 1 表示男性，2 表示女性。

-   要将数值装入存储桶，并希望为范围给出一个说明性名称。

-   要简化长名称。

## <a name="using-the-relabel-wizard"></a>使用重新标记向导

1.  在 "**数据挖掘**" 功能区中，单击 "**清除**"，然后选择 "**重新标记**"。

2.  选择具有要修复的数据的表或数据范围。

3.  在向导的 "**重新标记**" 页中，选择单个列，方法是从下拉列表中选择列，或者单击 "**数据示例**" 窗格中的列。

     "**数据示例**" 窗格只显示大约50行的数据，但会进行采样以确保看到的值很好。

     单击 "**计数**" 列标题，按每个值的计数进行排序。

     你还可以按**原始标签**排序，如果你想要先重新标记所有最高值或最低值，这很方便。

4.  在向导的 "**重新标记**数据" 页中，查看 "**原始标签**" 列中的值，并决定要如何分组或编辑这些值。

5.  在 "**新标签**" 下的行中键入新值。 您还可以从现有值列表中选择值。 随着您键入新值，这些值将立即可供重复使用。

6.  输入足够的行后，单击 "**下一步**"，然后在 "**选择目标**" 页上，选择保存重新标记数据的位置。

    -   **作为新列添加到当前工作表**

         单击此选项可将包含新值的新列添加到表中。

    -   **将工作表数据及其更改复制到新工作表**

         单击此选项可创建一个包含更新数据的新工作表。

    -   **就地更改数据**

         单击此选项可将原始数据替换为新值。

## <a name="see-also"></a>另请参阅
 [浏览和清除数据](exploring-and-cleaning-data.md)


