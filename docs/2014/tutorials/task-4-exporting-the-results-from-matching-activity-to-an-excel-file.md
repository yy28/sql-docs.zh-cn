---
title: 任务4：将匹配活动的结果导出到 Excel 文件 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 644454c4-3c5a-469a-90ec-e51dc7fb99fc
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 4ed1d29af328a162eafadb1ce7a160c262bdcba3
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2020
ms.locfileid: "78177245"
---
# <a name="task-4-exporting-the-results-from-matching-activity-to-an-excel-file"></a>任务 4：将匹配活动的结果导出到 Excel 文件
  在本任务中，您将匹配活动的结果导出到 Excel 文件。

1.  在 "**导出**" 页中，选择 " **Excel 文件**" 作为**目标类型**。

2.  选择**存活结果**选项。 在存活过程中，DQS 根据所选的**存活规则**确定每个群集的存活记录。

3.  单击 "**浏览**" 并导航到要在其中存储输出文件的文件夹。

4.  键入 "**清理"，并**将 "名称" 与 "名称" 匹配，并单击 "**打开**"。

5.  确认为**存活规则**选择了 "**透视记录**"。 当您选择此选项时，为分类的输出选择每个分类的透视记录。 存留规则的其他选项有：

    1.  **最完整记录：** 存活记录是具有最大填充字段数的记录。

    2.  **最长记录：** 存活记录是源字段中具有最大字词数的记录。

    3.  **最完整且最长的记录：** 存活记录是具有最大填充字段数的记录，每个字段中的字词数最多。

     ![从“匹配”页导出结果](../../2014/tutorials/media/et-exportingtheresultsfrommatoanexcelfile.jpg "从“匹配”页导出结果")

6.  单击 "**导出**" 将结果导出到 Excel 文件中。

7.  单击 "**关闭**" 以关闭 "**匹配导出**" 对话框。

8.  单击 "**完成**" 以完成匹配活动。

9. 打开**清理和匹配的供应商 .xlsx**文件，并确认看不到任何重复项（供应商）。

 现在，您的供应商数据已经过清理和匹配，删除了重复项。

## <a name="next-step"></a>下一步
 [第 4 课：在 MDS 中存储供应商数据](../../2014/tutorials/lesson-4-storing-supplier-data-in-mds.md)


