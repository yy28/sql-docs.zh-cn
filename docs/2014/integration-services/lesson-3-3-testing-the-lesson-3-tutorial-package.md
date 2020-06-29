---
title: 步骤 3：测试第 3 课教程包 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 1096a476-93cf-4474-86f5-27d6357eb380
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6ffa1849e099e670b5fa13db399af67883e8806c
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/26/2020
ms.locfileid: "85440464"
---
# <a name="step-3-testing-the-lesson-3-tutorial-package"></a>步骤 3：测试第 3 课教程包
  在该任务中，将运行 Lesson 3.dtsx 包。 在包运行时，“日志事件”窗口将列出写入日志文件中的日志条目。 执行完包之后，将验证日志提供程序所生成的日志文件的内容。  
  
## <a name="checking-the-package-layout"></a>检查包布局  
 测试包之前，应当确保 Lesson 3 包中的控制流和数据流包含下列关系图中显示的对象。 控制流应与第 2 课中的控制流相同。 数据流应与第 1 课和第 2 课中的数据流相同。  
  
 **控制流**  
  
 ![包中的控制流](../../2014/tutorials/media/task4lesson2control.gif "包中的控制流")  
  
 数据流  
  
 ![包中的数据流](../../2014/tutorials/media/task9lesson1data.gif "包中的数据流")  
  
### <a name="to-run-the-lesson-4-tutorial-package"></a>运行第 4 课教程包  
  
1.  在 SSIS 菜单中，单击“日志事件”。  
  
2.  在 **“调试”** 菜单中，单击 **“启动调试”**。  
  
3.  当包运行完毕后，在 **“调试”** 菜单中，单击 **“停止调试”**。  
  
### <a name="to-examine-the-generated-log-file"></a>检查生成的日志文件  
  
-   使用记事本或其他任何文本编辑器，打开 TutorialLog.log 文件。  
  
-   尽管为和事件生成的信息的语义 `PipelineExecutionPlan` `PipelineExecutionTrees` 超出了本教程的范围，但你可以看到第一行列出了在 "**配置 SSIS 日志**" 对话框的 "**详细信息**" 选项卡中指定的信息字段。 此外，可以验证已为 Foreach 循环的每个迭代记录了所选择的两个事件：PipelineExecutionPlan 和 PipelineExecutionTrees。  
  
## <a name="next-lesson"></a>下一课  
 [第 4 课：添加错误流重定向](../integration-services/lesson-4-add-error-flow-redirection-with-ssis.md)  
  
  
