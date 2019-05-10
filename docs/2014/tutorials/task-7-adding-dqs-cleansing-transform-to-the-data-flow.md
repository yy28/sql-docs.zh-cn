---
title: 任务 7：将 DQS 清理转换向数据流添加 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 0b749c71-dfb6-493a-804f-600290d46eef
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 209659609c2cf19196cc35050fb32e39e079d1c7
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65488946"
---
# <a name="task-7-adding-dqs-cleansing-transform-to-the-data-flow"></a>任务 7：将 DQS 清理转换添加到数据流
  在本任务中，您将向数据流添加 DQS 清理转换以使用 DQS 清理输入的供应商数据。 请参阅 **[DQS 清理转换](https://msdn.microsoft.com/library/ee677619.aspx)** 有关转换的详细信息。  
  
1.  右键单击**DQS 清理**中**数据流**选项卡，然后单击**重命名**。 类型**清理供应商数据**，然后按**ENTER**。  
  
2.  选择**从 Excel 文件读取供应商数据**; 将为蓝色连接器拖**清理供应商数据**。 组件现在已连接。  
  
     ![读取供应商数据-> 清理供应商数据](../../2014/tutorials/media/et-addingdqscleansingtransformtothedataflow-01.jpg "读取供应商数据-> 清理供应商数据")  
  
3.  双击**清理供应商数据**。  
  
4.  在中**DQS 清理转换编辑器**，单击**新建**旁边**数据质量连接管理器下拉列表**。  
  
5.  在中**DQS 清除连接管理器**对话框中，键入 **(local)** 或**期**（.） 以连接到本地服务器。 本课假定您在本地服务器上安装了 DQS。  
  
6.  单击**测试连接**以测试与 DQS 服务器的连接。  
  
7.  单击 **“确定”** 关闭对话框。  
  
8.  选择**供应商**有关**数据质量知识库**。  
  
     ![DQS 清理转换编辑器-供应商知识库](../../2014/tutorials/media/et-addingdqscleansingtransformtothedataflow-02.jpg "DQS 清理转换编辑器-供应商知识库")  
  
9. 切换到**映射**顶部选项卡。  
  
10. 从**可用输入列**，选择**Supplier Name**， **ContactEmailAddress**， **Address Line**，**城市**，**状态**，**国家/地区**，并且**邮政编码**通过选中复选框。  
  
     ![DQS 清除转换编辑器-映射](../../2014/tutorials/media/et-addingdqscleansingtransformtothedataflow-03.jpg "DQS 清理转换编辑器-映射")  
  
11. 使用下拉列表中的，在底部窗格中，映射这些列**域**列：  
  
    |“列”|域|  
    |------------|------------|  
    |Supplier Name|Supplier Name|  
    |ContactEmailAddress|Contact Email|  
    |Address Line|Address Line|  
    |City|City|  
    |State|State|  
    |Country|Country|  
    |Zip Code|Zip|  
  
12. 单击**确定**以关闭**DQS 清理转换编辑器**对话框。  
  
## <a name="next-step"></a>下一步  
 [任务 8:添加有条件拆分转换以拆分清理输出](../../2014/tutorials/task-8-adding-conditional-split-transform-to-split-cleansing-output.md)  
  
  
