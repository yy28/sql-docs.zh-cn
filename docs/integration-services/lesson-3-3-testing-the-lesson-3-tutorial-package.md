---
title: "步骤 3： 测试第 3 课教程包 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 1096a476-93cf-4474-86f5-27d6357eb380
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: d6477267c95ffd200f70b2c93191dfaf0883a4af
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="lesson-3-3---testing-the-lesson-3-tutorial-package"></a>Lesson 3-3-测试第 3 课教程包
在该任务中，将运行 Lesson 3.dtsx 包。 在包运行时，“日志事件”窗口将列出写入日志文件中的日志条目。 执行完包之后，将验证日志提供程序所生成的日志文件的内容。  
  
## <a name="checking-the-package-layout"></a>检查包布局  
测试包之前，应当确保 Lesson 3 包中的控制流和数据流包含下列关系图中显示的对象。 控制流应与第 2 课中的控制流相同。 数据流应与第 1 课和第 2 课中的数据流相同。  
  
**控制流**  
  
![控制包中的流](../integration-services/media/task4lesson2control.gif "控制包中的流")  
  
**数据流**  
  
![包中的数据流](../integration-services/media/task9lesson1data.gif "包中的数据流")  
  
### <a name="to-run-the-lesson-4-tutorial-package"></a>运行第 4 课教程包  
  
1.  在 SSIS 菜单中，单击“日志事件”。  
  
2.  在 **“调试”** 菜单中，单击 **“启动调试”**。  
  
3.  当包运行完毕后，在 **“调试”** 菜单中，单击 **“停止调试”**。  
  
### <a name="to-examine-the-generated-log-file"></a>检查生成的日志文件  
  
-   使用记事本或其他任何文本编辑器，打开 TutorialLog.log 文件。  
  
-   尽管为 **PipelineExecutionPlan** 和 **PipelineExecutionTrees** 事件所生成的信息的语义超出了本教程的讨论范围，但是，可以看到第一行列出了在 **“配置 SSIS 日志”** 对话框的 **“详细信息”** 选项卡中所指定的信息字段。 此外，可以验证已为 Foreach 循环的每个迭代记录了所选择的两个事件：PipelineExecutionPlan 和 PipelineExecutionTrees。  
  
## <a name="next-lesson"></a>下一课  
[第 4 课：使用 SSIS 添加错误流重定向](../integration-services/lesson-4-add-error-flow-redirection-with-ssis.md)  
  
  
  

