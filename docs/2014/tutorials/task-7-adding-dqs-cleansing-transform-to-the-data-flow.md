---
title: 任务 7： 添加 DQS 清除转换到数据流 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0b749c71-dfb6-493a-804f-600290d46eef
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 10b0fb12ace5a113bbde03cecf803a37b49b1974
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36137885"
---
# <a name="task-7-adding-dqs-cleansing-transform-to-the-data-flow"></a>任务 7：将 DQS 清理转换添加到数据流
  在本任务中，您将向数据流添加 DQS 清理转换以使用 DQS 清理输入的供应商数据。 请参阅 **[DQS 清理转换](http://msdn.microsoft.com/library/ee677619.aspx)** 转换有关的更多详细信息。  
  
1.  右键单击**DQS 清理**中**数据流**卡，然后单击**重命名**。 类型**清理供应商数据**，按**ENTER**。  
  
2.  选择**读取从 Excel 文件的供应商数据**; 拖动到蓝色连接器**清理供应商数据**。 组件现在已连接。  
  
     ![读取供应商数据-> 清理供应商数据](../../2014/tutorials/media/et-addingdqscleansingtransformtothedataflow-01.jpg "读取供应商数据-> 清理供应商数据")  
  
3.  双击**清理供应商数据**。  
  
4.  在**DQS 清理转换编辑器**，单击**新建**旁边**数据质量连接管理器下拉列表**。  
  
5.  在**DQS 清除连接管理器**对话框中，键入 **（本地）** 或**段**（.） 连接到本地服务器。 本课假定您在本地服务器上安装了 DQS。  
  
6.  单击**测试连接**到 DQS 服务器对连接进行测试。  
  
7.  单击 **“确定”** 关闭对话框。  
  
8.  选择**供应商**为**数据质量知识库**。  
  
     ![DQS 清除转换编辑器-供应商 KB](../../2014/tutorials/media/et-addingdqscleansingtransformtothedataflow-02.jpg "DQS 清除转换编辑器-供应商 KB")  
  
9. 切换到**映射**顶部的选项卡。  
  
10. 从**可用输入列**，选择**供应商名称**， **ContactEmailAddress**，**地址行**，**城市**，**状态**，**国家/地区**，和**邮政编码**通过选中复选框。  
  
     ![DQS 清除转换编辑器-映射](../../2014/tutorials/media/et-addingdqscleansingtransformtothedataflow-03.jpg "DQS 清除转换编辑器-映射")  
  
11. 在底部窗格中，通过使用下拉列表中的映射这些列**域**列：  
  
    |“列”|域|  
    |------------|------------|  
    |Supplier Name|Supplier Name|  
    |ContactEmailAddress|Contact Email|  
    |Address Line|Address Line|  
    |City|City|  
    |State|State|  
    |Country|Country|  
    |Zip Code|Zip|  
  
12. 单击**确定**关闭**DQS 清理转换编辑器**对话框。  
  
## <a name="next-step"></a>下一步  
 [任务 8：添加有条件拆分转换以拆分清理输出](../../2014/tutorials/task-8-adding-conditional-split-transform-to-split-cleansing-output.md)  
  
  