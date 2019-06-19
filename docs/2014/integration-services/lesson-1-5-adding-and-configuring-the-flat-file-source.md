---
title: 步骤 5：添加并配置平面文件源 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5c95ce51-e0fe-4fc5-95eb-2945929f2b13
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 32b95a5d156ae52394b7128b024c86b9a7e308b1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62891535"
---
# <a name="step-5-adding-and-configuring-the-flat-file-source"></a>步骤 5：添加并配置平面文件源
  在此任务中，将向包中添加一个平面文件源并对其进行配置。 平面文件源是一个数据流组件，它使用平面文件连接管理器定义的元数据来指定转换过程要从此平面文件中提取的数据的格式和结构。 可以通过使用平面文件连接管理器提供的文件格式定义将平面文件源配置为从单个平面文件提取数据。  
  
 对于本教程中，您将配置要使用的平面文件源`Sample Flat File Source Data`以前创建的连接管理器。  
  
### <a name="to-add-a-flat-file-source-component"></a>添加平面文件源组件  
  
1.  打开**数据流**设计器中，方法是双击`Extract Sample Currency Data`数据流任务或单击**数据流选项卡**。  
  
2.  在“SSIS 工具箱”  中，展开 **OtherSources**，然后将“平面文件源”  拖动到“数据流”  选项卡的设计图面上。  
  
3.  上**Data Flow**设计图面上，右键单击新添加**平面文件源**，单击**重命名**，并将名称更改为`Extract Sample Currency Data`。  
  
4.  双击此平面文件源，打开“平面文件源编辑器”对话框。  
  
5.  在中**平面文件连接管理器**框中，选择`Sample Flat File Source Data`。  
  
6.  单击“列”  并验证列名是否正确。  
  
7.  单击“确定”  。  
  
8.  右键单击“平面文件源”并单击“属性”  。  
  
9. 在属性窗口中，验证是否`LocaleID`属性设置为**英语 （美国）** 。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [步骤 6：添加并配置查找转换](lesson-1-6-adding-and-configuring-the-lookup-transformations.md)  
  
## <a name="see-also"></a>请参阅  
 [平面文件源](data-flow/flat-file-source.md)   
 [平面文件连接管理器编辑器（“常规”页）](general-page-of-integration-services-designers-options.md)  
  
  
