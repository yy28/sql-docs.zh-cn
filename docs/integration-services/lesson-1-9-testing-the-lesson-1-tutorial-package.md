---
title: "步骤 9： 测试第 1 课教程包 |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 9aee7acf-797b-46f2-830d-80ab64a9f0b6
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ca45e8e1ba02246eb5429bd7bfea125663f69f41
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="lesson-1-9---testing-the-lesson-1-tutorial-package"></a>课程 1-9-测试第 1 课教程包
在本课中，已经完成了下列任务：  
  
-   创建了一个新的 [!INCLUDE[ssIS](../includes/ssis-md.md)] 项目。  
  
-   配置了包连接到源数据和目标数据所需的连接管理器。  
  
-   添加了一个数据流，该数据流从平面文件源提取数据，对数据执行必要的查找转换，并为目标配置数据。  
  
包现在已经完成了！ 该对包进行测试了。  
  
## <a name="checking-the-package-layout"></a>检查包布局  
测试包之前，应当确保 Lesson 1 包中的控制流和数据流包含下列关系图中显示的对象。  
  
**控制流**  
  
![控制包中的流](../integration-services/media/task9lesson1control.gif "控制包中的流")  
  
**数据流**  
  
![包中的数据流](../integration-services/media/task9lesson1data.gif "包中的数据流")  
  
### <a name="to-run-the-lesson-1-tutorial-package"></a>运行 Lesson 1 教程包  
  
1.  在 **“调试”** 菜单中，单击 **“启动调试”**。  
  
    包将开始运行，结果有 1097 个行被成功添加到 **AdventureWorksDW2012** 中的 **FactCurrency**事实数据表中。  
  
2.  当包运行完毕后，在 **“调试”** 菜单中，单击 **“停止调试”**。  
  
## <a name="next-lesson"></a>下一课  
[第 2 课：使用 SSIS 添加循环](../integration-services/lesson-2-adding-looping-with-ssis.md)  
  
## <a name="see-also"></a>另请参阅  
[项目和包的执行](https://msdn.microsoft.com/library/ms141708(v=sql.110).aspx) 
  
  
  

