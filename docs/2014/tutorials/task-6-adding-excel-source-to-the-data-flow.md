---
title: 任务6：将 Excel 源添加到数据流 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 0209055e-cb6b-4a07-909e-836596727a2c
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 92a4c3e650ce375a1e80079bbad83c5ab2b9bcd9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68495285"
---
# <a name="task-6-adding-excel-source-to-the-data-flow"></a>任务 6：将 Excel 源添加到数据流
  在本任务中，您向数据流添加 Excel 源，以便从源 Excel 文件读取供应商数据。 Excel 源从 Microsoft Excel 工作簿的工作表或范围中提取数据。 有关更多详细信息，请参阅[Excel 源](../integration-services/data-flow/excel-source.md)主题。  
  
1.  将 " **Excel 源**" 从 **"SSIS 工具箱**" 中的**其他源**拖放到 "数据流 **" 选项卡**。  
  
2.  右键单击 "数据流 **" 选项卡**中的 " **Excel 源**"，然后单击 "**重命名**"。  
  
3.  键入 "**从 Excel 文件读取供应商数据**"，然后按**enter**。  
  
4.  双击 "**从 Excel 文件读取供应商数据**" 以启动 " **excel 源编辑器**" 对话框。  
  
5.  在 " **Excel 源编辑器**" 对话框中，单击 "**新建**" 以创建 Excel 连接。  
  
6.  在 " **Excel 连接管理器**" 对话框中，单击 "**浏览**"，然后选择**EIM 教程**文件夹中的 "**供应商 .xls** " 文件。 确认在 " **Excel 版本**" 框中选择了 " **Microsoft Excel 97-2003** "，然后单击 **"确定"**。  
  
     ![“Excel 连接管理器”对话框](../../2014/tutorials/media/et-addingexcelsourcetothedataflow-01.jpg "“Excel 连接管理器”对话框")  
  
7.  在 " **Excel 源编辑器**" 对话框中，选择 " **excel 工作表**" 列表框名称中的 " **IncomingSuppliers $** "。  
  
     ![Excel 工作表的名称 - 传入的供应商$](../../2014/tutorials/media/et-addingexcelsourcetothedataflow-02.jpg "Excel 工作表的名称 - 传入的供应商$")  
  
8.  单击 "**预览**" 以预览 Excel 文件中的数据。  
  
9. 单击 **“确定”** 关闭对话框。  
  
10. 将 " **SSIS 工具箱**" 中 "**其他转换**" 中的 " **DQS 清理**转换" 拖放到 "**从 Excel 文件读取供应商数据**" 下的 "**数据流**" 选项卡。 DQS 清理转换将通过 Data Quality Services (DQS) 应用知识库中已批准的规则来更正数据。 此转换在运行时会在 DQS 服务器上创建一个 DQS 清理项目。 有关更多详细信息，请参阅[DQS 清理转换](https://msdn.microsoft.com/library/ee677619.aspx)主题。  
  
## <a name="next-step"></a>下一步

[任务 7：将 DQS 清理转换添加到数据流](task-7-adding-dqs-cleansing-transform-to-the-data-flow.md)  

### <a name="see-also"></a>另请参阅

[数据流](../integration-services/data-flow/data-flow.md)  
