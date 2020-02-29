---
title: 任务6：设置同义词 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: b7d35ee9-d1c9-41d9-bbc5-0ca7db93e54d
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 4499a0a099c92a9b1802cc905da3d0a473808eeb
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/28/2020
ms.locfileid: "78177225"
---
# <a name="task-6-setting-synonyms"></a>任务 6：设置同义词
  在此任务中，您将**国家/地区**域的两个域值（ **USA**和**美国**）设置为具有**美国**作为前导值的同义词。 由于在创建**国家/地区**域时选择了 "**使用前导值**" 选项，因此**国家/地区**域的任何**USA**值都将作为**美国**输出（因为美国是前导值）。 有关更多详细信息，请参阅[更改域值](https://msdn.microsoft.com/library/hh510408.aspx)。

1.  从域列表中选择 "**国家/地区**"。

2.  切换到 "**域值**" 选项卡。

3.  单击工具栏上的 "**添加新的域值**" 按钮。

4.  键入**USA**作为值，然后按**enter**。

5.  使用 CTRL 或 SHIFT 键的多选项**美国**和**美国**，右键单击所选项，然后单击 "**设为同义词**"。 DQS 将对这些值进行分组，然后将这些值之一指定为将用来替换其他值的前导值。

     ![“设为同义词”菜单](../../2014/tutorials/media/et-settingsynonyms-01.jpg "“设为同义词”菜单")

6.  请注意，**美国**设置为前导值。 如果希望 USA 成为前导值，则可以右键单击 "USA"，然后选择 "**设置为前导**" 选项。 对于本教程，我们将**美国**用作前导值。

     ![美国和 USA 为同义词](../../2014/tutorials/media/et-settingsynonyms-02.jpg "美国和 USA 为同义词")

## <a name="next-step"></a>下一步
 [任务 7：创建复合域规则](../../2014/tutorials/task-7-creating-a-composite-domain.md)


