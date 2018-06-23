---
title: 任务 6： 将 Excel 源添加到数据流 |Microsoft 文档
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
ms.assetid: 0209055e-cb6b-4a07-909e-836596727a2c
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 1cde5dc49851e7d8c808d4a6273f4d4caf6603e2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36138973"
---
# <a name="task-6-adding-excel-source-to-the-data-flow"></a>任务 6：将 Excel 源添加到数据流
  在本任务中，您向数据流添加 Excel 源，以便从源 Excel 文件读取供应商数据。 Excel 源从 Microsoft Excel 工作簿的工作表或范围中提取数据。 请参阅[Excel 源](http://msdn.microsoft.com/library/ms141683.aspx)更多详细信息的主题。  
  
1.  拖放**Excel 源**从**其他源**中**SSIS 工具箱**到**数据流**选项卡。  
  
2.  右键单击**Excel 源**中**数据流**卡，然后单击**重命名**。  
  
3.  类型**读取从 Excel 文件的供应商数据**按**ENTER**。  
  
4.  双击**读取从 Excel 文件的供应商数据**以启动**Excel 源编辑器**对话框。  
  
5.  在**Excel 源编辑器**对话框中，单击**新建**要创建 Excel 连接。  
  
6.  在**Excel 连接管理器**对话框中，单击**浏览**，然后选择**Suppliers.xls**文件中**EIM 教程**文件夹. 确认**Microsoft Excel 97-2003年**中选择**Excel 版本**中，然后单击**确定**。  
  
     ![Excel 连接管理器对话框](../../2014/tutorials/media/et-addingexcelsourcetothedataflow-01.jpg "Excel 连接管理器对话框")  
  
7.  在**Excel 源编辑器**对话框中，选择**IncomingSuppliers$** 中**Excel 表的名称**列表框。  
  
     ![名称的 Excel 工作表的传入供应商 $](../../2014/tutorials/media/et-addingexcelsourcetothedataflow-02.jpg "Excel 表-传入的供应商 $ 的名称")  
  
8.  单击**预览**预览 Excel 文件中的数据。  
  
9. 单击 **“确定”** 关闭对话框。  
  
10. 拖放**DQS 清理**在中转换**其他转换**上**SSIS 工具箱**到**数据流**下**从 Excel 文件读取供应商数据**。 DQS 清理转换将通过 Data Quality Services (DQS) 应用知识库中已批准的规则来更正数据。 此转换在运行时会在 DQS 服务器上创建一个 DQS 清理项目。 请参阅[DQS 清除转换](http://msdn.microsoft.com/library/ee677619.aspx)更多详细信息的主题。  
  
## <a name="next-step"></a>下一步  
 [任务 7：将 DQS 清理转换添加到数据流](../integration-services/data-flow/data-flow.md)  
  
  