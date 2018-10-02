---
title: 步骤 5：添加并配置平面文件源 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 5c95ce51-e0fe-4fc5-95eb-2945929f2b13
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3417579b121d4680b18cfd896bb3ddd676eca920
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47600445"
---
# <a name="lesson-1-5---adding-and-configuring-the-flat-file-source"></a>第 1-5 课 - 添加并配置平面文件源
在此任务中，将向包中添加一个平面文件源并对其进行配置。 平面文件源是一个数据流组件，它使用平面文件连接管理器定义的元数据来指定转换过程要从此平面文件中提取的数据的格式和结构。 可以通过使用平面文件连接管理器提供的文件格式定义将平面文件源配置为从单个平面文件提取数据。  
  
对于本教程，你将把平面文件源配置为使用以前创建的 **Sample Flat File Source Data** 连接管理器。  
  
### <a name="to-add-a-flat-file-source-component"></a>添加平面文件源组件  
  
1.  打开“数据流”设计器，方法是双击 **Extract Sample Currency Data** 数据流任务或单击“数据流”选项卡。  
  
2.  在“SSIS 工具箱”中，展开 **OtherSources**，然后将“平面文件源”拖动到“数据流”选项卡的设计图面上。  
  
3.  在“数据流”设计图面上，右键单击新添加的“平面文件源”，单击“重命名”，然后将该名称改为 **Extract Sample Currency Data**。  
  
4.  双击此平面文件源，打开“平面文件源编辑器”对话框。  
  
5.  在“平面文件连接管理器”框中，选择 **Sample Flat File Source Data**。  
  
6.  单击“列”并验证列名是否正确。  
  
7.  单击“确定” 。  
  
8.  右键单击“平面文件源”并单击“属性”。  
  
9. 在“属性”窗口中，验证是否已将 **LocaleID** 属性设置为“英语(美国)”。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
[步骤 6：添加并配置查找转换](../integration-services/lesson-1-6-adding-and-configuring-the-lookup-transformations.md)  
  
## <a name="see-also"></a>另请参阅  
[平面文件源](../integration-services/data-flow/flat-file-source.md)  
[平面文件连接管理器编辑器（“常规”页）](../integration-services/connection-manager/flat-file-connection-manager-editor-general-page.md)  
  
  
  
