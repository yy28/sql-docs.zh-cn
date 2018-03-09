---
title: "步骤 4：添加平面文件目标 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: f4088de3-16d8-419c-96a1-a2cd005d0a5b
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d9024e237d159c37b18a89be62b0982149c81253
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="lesson-4-4---adding-a-flat-file-destination"></a>第 4-4 课 - 添加平面文件目标
Lookup Currency Key 转换的错误输出将无法执行查找操作的所有数据行重定向到脚本转换。 为了突显相关错误的信息，脚本转换将运行可获取错误说明的脚本。  
  
在本任务中，请将有关失败行的所有这些信息保存到分隔的文件中，以便进行后续处理。 若要保存失败的行，必须为将包含错误数据和平面文件目标的文本文件添加并配置平面文件连接管理器。 通过设置平面文件目标所用平面文件连接管理器的属性，可以指定平面文件目标如何格式化和写入文本文件。 有关详细信息，请参阅 [平面文件连接管理器](../integration-services/connection-manager/flat-file-connection-manager.md) 和 [平面文件目标](../integration-services/data-flow/flat-file-destination.md)。  
  
### <a name="to-add-and-configure-a-flat-file-destination"></a>添加并配置平面文件目标  
  
1.  单击 **“数据流”** 选项卡。  
  
2.  在“SSIS 工具箱”中，展开“其他”，然后将“平面文件目标”拖动到数据流设计图面上。 将“平面文件目标”直接放在“获取错误说明”转换的下面。  
  
3.  单击“获取错误说明”转换，然后将绿色箭头拖动到新的“平面文件目标”上。  
  
4.  在“数据流”设计图面上，在新添加的“平面文件目标”转换中单击“平面文件目标”，然后将该名称更改为 **Failed Rows**。  
  
5.  右键单击 **Failed Rows** 转换，再单击“编辑”，然后在”平面文件目标编辑器”中单击“新建”。  
  
6.  在“平面文件格式”对话框中，确认已选中“带分隔符”，然后单击“确定”。  
  
7.  在“平面文件连接管理器编辑器”的“连接管理器名称”框中，输入 **Error Data**。  
  
8.  在“平面文件连接管理器编辑器”对话框中，单击“浏览”，然后找到存储文件的文件夹。  
  
9. 在“打开”对话框中，对于“文件名”输入 **ErrorOutput.txt**，然后单击“打开”。  
  
10. 在“平面文件连接管理器编辑器”对话框中，验证“区域设置”框是否包含“英语(美国)”，“代码页”是否包含 1252 (ANSI -Latin I)。  
  
11. 在“选项”窗格中，单击“列”。  
  
    注意，除了源数据文件中的列以外，还存在三个新列：ErrorCode、ErrorColumn 和 ErrorDescription。 这三列由 Lookup Currency Key 转换的错误输出和获取错误说明转换中的脚本生成，可用于排查失败行的原因。  
  
12. 单击“确定” 。  
  
13. 在“平面文件目标编辑器”中，清除“覆盖文件中的数据”复选框。  
  
    清除该复选框可使错误在执行多个包的过程中持续存在。  
  
14. 在“平面文件目标编辑器”中，单击“映射”来验证所有列是否正确。 您也可以选择重命名目标中的列。  
  
15. 单击“确定” 。  
  
## <a name="next-steps"></a>Next Steps  
[步骤 5：测试第 4 课教程包](../integration-services/lesson-4-5-testing-the-lesson-4-tutorial-package.md)  
  
  
  
