---
title: 任务7：将 DQS 清理转换添加到数据流 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 0b749c71-dfb6-493a-804f-600290d46eef
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 0978452104eb9a55d49dfa9f851ef7578489db26
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85006483"
---
# <a name="task-7-adding-dqs-cleansing-transform-to-the-data-flow"></a>任务 7：将 DQS 清理转换添加到数据流
  在本任务中，您将向数据流添加 DQS 清理转换以使用 DQS 清理输入的供应商数据。 有关转换的详细信息，请参阅**[DQS 清理转换](https://msdn.microsoft.com/library/ee677619.aspx)**。  
  
1.  右键**单击 "数据流**" 选项卡中的 " **DQS 清理**"，然后单击 "**重命名**"。 键入 "**清理供应商数据**"，然后按**enter**。  
  
2.  选择 "**从 Excel 文件读取供应商数据**"。拖动蓝色连接器以**清理供应商数据**。 组件现在已连接。  
  
     ![读取供应商数据-> 清理供应商数据](../../2014/tutorials/media/et-addingdqscleansingtransformtothedataflow-01.jpg "读取供应商数据 -> 清理供应商数据")  
  
3.  双击 "**清理供应商数据**"。  
  
4.  在 " **DQS 清理转换编辑器**" 中，单击 "**数据质量连接管理器" 下拉列表**旁边的 "**新建**"。  
  
5.  在 " **DQS 清理连接管理器**" 对话框中，键入 **（local）** 或**句点**（.）以连接到本地服务器。 本课假定您在本地服务器上安装了 DQS。  
  
6.  单击 "**测试连接**" 以测试与 DQS 服务器的连接。  
  
7.  单击“确定”  关闭对话框。  
  
8.  选择**数据质量知识库**的 "**供应商**"。  
  
     ![DQS 清理转换编辑器 - 供应商知识库](../../2014/tutorials/media/et-addingdqscleansingtransformtothedataflow-02.jpg "DQS 清理转换编辑器 - 供应商知识库")  
  
9. 切换到顶部的 "**映射**" 选项卡。  
  
10. 在 "**可用输入列**" 中，通过选中相应的复选框来选择**供应商名称**、 **ContactEmailAddress**、**地址行**、**城市**、**省**/市/自治区、**国家/地区**和**邮政编码**。  
  
     ![DQS 清理转换编辑器 - 映射](../../2014/tutorials/media/et-addingdqscleansingtransformtothedataflow-03.jpg "DQS 清理转换编辑器 - 映射")  
  
11. 在底部窗格中，使用 "**域**" 列中的下拉列表映射这些列：  
  
    |列|域|  
    |------------|------------|  
    |Supplier Name|Supplier Name|  
    |ContactEmailAddress|联系人电子邮件|  
    |Address Line|Address Line|  
    |城市|城市|  
    |状态|状态|  
    |国家/地区|国家/地区|  
    |Zip Code|Zip|  
  
12. 单击 **"确定"** 关闭 " **DQS 清理转换编辑器**" 对话框。  
  
## <a name="next-step"></a>后续步骤  
 [任务 8：添加有条件拆分转换以拆分清理输出](../../2014/tutorials/task-8-adding-conditional-split-transform-to-split-cleansing-output.md)  
  
  
