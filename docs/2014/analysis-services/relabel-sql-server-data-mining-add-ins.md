---
title: 重新标记发生 （SQL Server 数据挖掘外接程序） |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- data preparation
- relabel
- data cleaning
ms.assetid: af041b39-fdd1-4cb5-a5ef-2f3ddab84614
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 50dd1a2c4cd425243c55ef9181387a08c5d935ba
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36127174"
---
# <a name="relabel-sql-server-data-mining-add-ins"></a>重新标记（SQL Server 数据挖掘外接程序）
  ![重新标记工具 office 13 图标](media/dm13-relabel.gif "重新标记工具 Office 13 图标")  
  
 使用 Excel 数据挖掘客户端可以为数据创建新标签，以便使分析结果更容易理解。  
  
 重新标记的原因包括：  
  
-   数据的结果经过编码，如 1 表示男性，2 表示女性。  
  
-   要将数值装入存储桶，并希望为范围给出一个说明性名称。  
  
-   要简化长名称。  
  
## <a name="using-the-relabel-wizard"></a>使用重新标记向导  
  
1.  在**数据挖掘**功能区上，单击**清理**，然后选择**重新标记**。  
  
2.  选择具有要修复的数据的表或数据范围。  
  
3.  在**重新标记**页的向导中，选择一个列中，通过从下拉列表中，选择列或通过单击中的列**数据样本**窗格。  
  
     **数据样本**窗格仅显示大约 50 行数据，但它们采样以确保你看到良好跨页的值。  
  
     单击列标题**计数**要作为排序依据每个值的计数。  
  
     此外可以通过排序**原始标签**，这是很方便，如果你想要重新首先标记所有上限或下限值。  
  
4.  在**重新标记**向导的数据页上查看中的值**原始标签**列，并决定你想要进行分组或对其进行编辑。  
  
5.  在下方的行中键入新值**新标签**。 您还可以从现有值列表中选择值。 随着您键入新值，这些值将立即可供重复使用。  
  
6.  当您输入足够行时，单击**下一步**，然后在**选择目标**页上，选择将在其中保存重新标记的数据。  
  
    -   **将作为新列添加到当前工作表**  
  
         单击此选项可将包含新值的新列添加到表中。  
  
    -   **将表数据及其更改复制到新工作表**  
  
         单击此选项可创建一个包含更新数据的新工作表。  
  
    -   **更改位置中的数据**  
  
         单击此选项可将原始数据替换为新值。  
  
## <a name="see-also"></a>请参阅  
 [浏览和清除数据](exploring-and-cleaning-data.md)  
  
  