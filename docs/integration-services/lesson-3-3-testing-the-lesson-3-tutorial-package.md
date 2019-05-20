---
title: 步骤 3：测试第 3 课教程包 | Microsoft Docs
ms.custom: ''
ms.date: 01/04/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 1096a476-93cf-4474-86f5-27d6357eb380
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5884506c83dfc0f3cbee6119ad9047807c35fbfe
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/16/2019
ms.locfileid: "65722086"
---
# <a name="lesson-3-3-test-the-lesson-3-tutorial-package"></a>第 3-3 课：测试第 3 课教程包

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



在该任务中，运行 Lesson 3.dtsx 包。 在包运行时，“日志事件”窗口会列出日志提供程序 SSIS 写入日志文件的日志条目。 在包完成执行后，可查看日志文件的内容。  
  
## <a name="check-the-package-layout"></a>检查包布局  
在测试包之前，请验证第 3 课程包中的控件和数据流是否与下图中显示的对象类似。 控制流应与第 2 课相同，数据流应与第 1 课和第 2 课相同。  
  
**控制流**  
  
![包中的控制流](../integration-services/media/task4lesson2control.gif "Control flow in package")  
  
**数据流**  
  
![包中的数据流](../integration-services/media/task9lesson1data.gif "Data flow in package")  
  
## <a name="run-the-lesson-3-tutorial-package"></a>运行第 3 课教程包  
  
1.  在“SSIS”菜单中，选择“日志事件”。  
  
2.  在“调试”菜单中，选择“启动调试”。  
  
3.  当包运行完毕后，在“调试”菜单中，选择“停止调试”。  
  
## <a name="examine-the-generated-log-file"></a>检查生成的日志文件  
  
-   使用记事本或其他任何文本编辑器，打开 TutorialLog.log 文件。  
  
-   为 PipelineExecutionPlan 和 PipelineExecutionTrees 事件生成的信息的完整说明不在本教程的范围内。  在日志文件中，可以看到第一行列出了“配置 SSIS 日志”对话框的“详细信息”选项卡中指定的信息字段。 还可以看见 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 为 Foreach 循环的每个迭代记录了所选的两个事件：PipelineExecutionPlan 和 PipelineExecutionTrees。  
  
## <a name="next-lesson"></a>下一课  
[第 4 课：使用 SSIS 添加错误流重定向](../integration-services/lesson-4-add-error-flow-redirection-with-ssis.md)  
  
  
  
