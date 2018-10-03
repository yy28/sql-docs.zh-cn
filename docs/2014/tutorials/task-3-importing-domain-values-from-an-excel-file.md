---
title: 任务 3： 从 Excel 文件导入域值 |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.topic: conceptual
ms.assetid: 242e8309-1195-495b-9cd5-aa127748c185
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 56aa693625ecf78ddd5084b88e6fd6c3e2e0f5b5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48215097"
---
# <a name="task-3-importing-domain-values-from-an-excel-file"></a>任务 3：从 Excel 文件导入域值
  在此任务中，导入的值**状态**域从 Excel 文件的工作表。  
  
1.  单击**状态**中的域**域列表**。  
  
2.  絋粄**域值**选项卡处于活动状态的右窗格中。  
  
3.  在右窗格中，从工具栏中，单击**向下箭头**旁边**导入值**按钮，然后单击**从 Excel 导入有效值**。  
  
     ![从 Excel 菜单导入有效值](../../2014/tutorials/media/et-importingdomainvaluesfromanexcelfile-01.jpg "从 Excel 菜单导入有效值")  
  
4.  单击**浏览**，选择**Suppliers.xls**，然后单击**打开**。  
  
5.  选择**StatesToImport$** 有关**工作表**。  
  
     ![导入域值对话框](../../2014/tutorials/media/et-importingdomainvaluesfromanexcelfile-02.jpg "导入域值对话框")  
  
6.  单击**确定**以关闭**导入域值**对话框。 您应在列表中看到导入的所有州的名称。 请注意，**仅显示新**导入后会自动选择选项。 当您导入值且在列表中看不到旧值时，这是因为导入后自动启用了此选项。 要查看所有值，请清除此复选框。 如果再次导入相同的一组值，则不导入任何值，因为它们在域中已存在。  
  
     ![对域值显示仅将新的复选框](../../2014/tutorials/media/et-importingdomainvaluesfromanexcelfile-03.jpg "对域值显示仅将新的复选框")  
  
## <a name="next-step"></a>下一步  
 [任务 4：设置域规则](../../2014/tutorials/task-4-setting-domain-rules.md)  
  
  
