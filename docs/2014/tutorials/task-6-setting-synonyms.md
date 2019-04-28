---
title: 任务 6:设置同义词 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: b7d35ee9-d1c9-41d9-bbc5-0ca7db93e54d
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: a81a538e2cd15dd38a6c32993395cac20079b6f2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62866325"
---
# <a name="task-6-setting-synonyms"></a>任务 6:设置同义词
  在本任务中，设置两个域值， **USA**并**美国**的**国家/地区**域为使用同义词**美国**为前导值。 由于**使用前导值**创建时选择了选项**国家/地区**域中，任何**USA**值**国家/地区**域将输出为**美国**（因为 United States 是前导值）。 请参阅[Change Domain Values](https://msdn.microsoft.com/library/hh510408.aspx)的更多详细信息。  
  
1.  选择**国家/地区**从域列表。  
  
2.  切换到**域值**选项卡。  
  
3.  单击**添加新的域值**工具栏上的按钮。  
  
4.  类型**USA**值并按**ENTER**。  
  
5.  多选**美国**并**USA**使用 CTRL 或 SHIFT 键，右键单击所选的项目，然后依次**设置为同义词**。 DQS 将对这些值进行分组，然后将这些值之一指定为将用来替换其他值的前导值。  
  
     ![将设置为同义词菜单](../../2014/tutorials/media/et-settingsynonyms-01.jpg "设为同义词菜单")  
  
6.  请注意，**美国**设置为前导值。 如果您希望 USA 是前导值，可以右键单击 USA，并选择**设置为主导**选项。 对于本教程中，我们使用**美国**为前导值。  
  
     ![美国和 USA 为同义词](../../2014/tutorials/media/et-settingsynonyms-02.jpg "美国和 USA 为同义词")  
  
## <a name="next-step"></a>下一步  
 [任务 7:创建复合域](../../2014/tutorials/task-7-creating-a-composite-domain.md)  
  
  
