---
title: 步骤 9：测试第 1 课教程包 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 9aee7acf-797b-46f2-830d-80ab64a9f0b6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ba98c694b99eb1ab81836a5d1f23a5cd4ea0d545
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48196997"
---
# <a name="step-9-testing-the-lesson-1-tutorial-package"></a>步骤 9：测试 Lesson 1 教程包
  在本课中，已经完成了下列任务：  
  
-   创建了一个新的 [!INCLUDE[ssIS](../includes/ssis-md.md)] 项目。  
  
-   配置了包连接到源数据和目标数据所需的连接管理器。  
  
-   添加了一个数据流，该数据流从平面文件源提取数据，对数据执行必要的查找转换，并为目标配置数据。  
  
 包现在已经完成了！ 该对包进行测试了。  
  
## <a name="checking-the-package-layout"></a>检查包布局  
 测试包之前，应当确保 Lesson 1 包中的控制流和数据流包含下列关系图中显示的对象。  
  
 **控制流**  
  
 ![包中的控制流](../../2014/tutorials/media/task9lesson1control.gif "Control flow in package")  
  
 **数据流**  
  
 ![包中的数据流](../../2014/tutorials/media/task9lesson1data.gif "Data flow in package")  
  
### <a name="to-run-the-lesson-1-tutorial-package"></a>运行 Lesson 1 教程包  
  
1.  在 **“调试”** 菜单中，单击 **“启动调试”**。  
  
     包将开始运行，结果有 1097 个行被成功添加到 **AdventureWorksDW2012** 中的 **FactCurrency**事实数据表中。  
  
2.  当包运行完毕后，在 **“调试”** 菜单中，单击 **“停止调试”**。  
  
## <a name="next-lesson"></a>下一课  
 [第 2 课：添加循环](../integration-services/lesson-2-adding-looping-with-ssis.md)  
  
## <a name="see-also"></a>请参阅  
 [项目和包的执行](packages/run-integration-services-ssis-packages.md)  
  
  
