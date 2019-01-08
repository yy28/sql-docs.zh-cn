---
title: 任务 6：将 Excel 源添加到数据流 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.topic: conceptual
ms.assetid: 0209055e-cb6b-4a07-909e-836596727a2c
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: bb79a52e8ce910425de44b5cf475400daa3f40aa
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/13/2018
ms.locfileid: "53356542"
---
# <a name="task-6-adding-excel-source-to-the-data-flow"></a>任务 6：将 Excel 源添加到数据流
  在本任务中，您向数据流添加 Excel 源，以便从源 Excel 文件读取供应商数据。 Excel 源从 Microsoft Excel 工作簿的工作表或范围中提取数据。 请参阅[Excel 源](../integration-services/data-flow/excel-source.md)主题的更多详细信息。  
  
1.  拖放**Excel 源**从**其他源**中**SSIS 工具箱**到**数据流**选项卡。  
  
2.  右键单击**Excel 源**中**数据流**选项卡，然后单击**重命名**。  
  
3.  类型**从 Excel 文件读取供应商数据**然后按**ENTER**。  
  
4.  双击**从 Excel 文件读取供应商数据**以启动**Excel 源编辑器**对话框。  
  
5.  在中**Excel 源编辑器**对话框中，单击**新建**创建 Excel 连接。  
  
6.  在中**Excel 连接管理器**对话框中，单击**浏览**，然后选择**Suppliers.xls**中的文件**EIM Tutorial**文件夹. 确认**Microsoft Excel 97-2003年**中选择**Excel 版本**框，然后单击**确定**。  
  
     ![Excel 连接管理器对话框](../../2014/tutorials/media/et-addingexcelsourcetothedataflow-01.jpg "Excel 连接管理器对话框")  
  
7.  在中**Excel 源编辑器**对话框中，选择**IncomingSuppliers$** 中**Excel 工作表的名称**列表框。  
  
     ![Excel 工作表-传入的供应商 $ 的名称](../../2014/tutorials/media/et-addingexcelsourcetothedataflow-02.jpg "Excel 工作表-传入的供应商 $ 的名称")  
  
8.  单击**预览版**以预览 Excel 文件中的数据。  
  
9. 单击 **“确定”** 关闭对话框。  
  
10. 拖放**DQS 清理**转换中**其他转换**上**SSIS 工具箱**到**数据流**选项卡上的**从 Excel 文件读取供应商数据**。 DQS 清理转换将通过 Data Quality Services (DQS) 应用知识库中已批准的规则来更正数据。 此转换在运行时会在 DQS 服务器上创建一个 DQS 清理项目。 请参阅[DQS 清除转换](https://msdn.microsoft.com/library/ee677619.aspx)主题的更多详细信息。  
  
## <a name="next-step"></a>下一步  
 [任务 7:添加 DQS 清理转换添加到数据流](../integration-services/data-flow/data-flow.md)  
  
  
