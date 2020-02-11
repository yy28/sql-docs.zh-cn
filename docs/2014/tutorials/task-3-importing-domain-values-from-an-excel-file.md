---
title: 任务3：从 Excel 文件导入域值 |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 242e8309-1195-495b-9cd5-aa127748c185
ms.author: lle
author: lrtoyou1223
ms.openlocfilehash: d86d71a3d62ca94eed2da5ad91fbdd60ee4989f4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66822987"
---
# <a name="task-3-importing-domain-values-from-an-excel-file"></a>任务 3：从 Excel 文件导入域值

  在此任务中，您将从 Excel 文件的工作表中导入**状态**域的值。  
  
1.  单击 "**域列表**" 中的 "**状态**域"。  
  
2.  确保右侧窗格中的 "**域值**" 选项卡处于活动状态。  
  
3.  在右侧窗格的工具栏中，单击 "**导入值**" 按钮旁边的**向下箭头**，然后单击 "**从 Excel 导入有效值**"。  
  
     ![“从 Excel 导入有效值”菜单](../../2014/tutorials/media/et-importingdomainvaluesfromanexcelfile-01.jpg "“从 Excel 导入有效值”菜单")  
  
4.  单击 "**浏览**" **，选择 "**"，然后单击 "**打开**"。  
  
5.  选择**工作表**的**StatesToImport $** 。  
  
     ![“导入域值”对话框](../../2014/tutorials/media/et-importingdomainvaluesfromanexcelfile-02.jpg "“导入域值”对话框")  
  
6.  单击 **"确定"** 以关闭 "**导入域值**" 对话框。 您应在列表中看到导入的所有州的名称。 请注意，在导入后会自动选择 "**仅显示新**选项"。 导入值后，在列表中看不到旧值，这是因为在导入后会自动启用此选项。 要查看所有值，请清除此复选框。 如果再次导入相同的一组值，则不导入任何值，因为它们在域中已存在。  
  
     ![仅显示域值的新复选框](../../2014/tutorials/media/et-importingdomainvaluesfromanexcelfile-03.jpg "仅显示域值的新复选框")  
  
## <a name="next-step"></a>下一步  
 [任务 4：设置域规则](../../2014/tutorials/task-4-setting-domain-rules.md)  
  
  
