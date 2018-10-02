---
title: 步骤 4：测试第 2 课教程包 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 0e8c0a25-8f79-41df-8ed2-f82a74b129cd
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 314e79b0cf5a35a27d93fc3a6906bdb9fbe01abc
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47745725"
---
# <a name="lesson-2-4---testing-the-lesson-2-tutorial-package"></a>第 2-4 课 - 测试第 2 课教程包
使用现在配置的 Foreach 循环容器和平面文件连接管理器，Lesson 2 包可以迭代遍历示例数据文件夹中由 14 个平面文件组成的集合。 每次找到与指定的文件名条件匹配的文件名时，Foreach 循环容器都将用该文件名填充用户定义的变量。 该变量又会更新平面文件连接管理器的 ConnectionString 属性，并与新平面文件建立连接。 然后，在连接到文件夹中的下一个文件之前，Foreach 循环容器将对新平面文件中的数据运行未修改的数据流任务。  
  
使用以下过程可以测试已添加到包中的新循环功能。  
  
> [!NOTE]  
> 如果您已运行第 1 课中的包，则在运行本课中的该包之前，您需要从 AdventureWorksDW2012 的 dbo.FactCurrency 中删除记录，否则包将失败，并出现指示主键约束冲突的错误。 如果您通过选择“调试”/“启动调试”（或按 F5）来运行包，则由于第 1 课和第 2 课都将运行该包，因此您会收到相同的错误。 第 2 课将尝试插入第 1 课中已插入的记录。  
  
## <a name="checking-the-package-layout"></a>检查包布局  
测试包之前，应当确保第 2 课包中的控制流和数据流包含下列关系图中显示的对象。 数据流应与第 1 课中的数据流相同。  
  
**控制流**  
  
![包中的控制流](../integration-services/media/task4lesson2control.gif "Control flow in package")  
  
**数据流**  
  
![包中的数据流](../integration-services/media/task9lesson1data.gif "Data flow in package")  
  
### <a name="to-test-the-lesson-2-tutorial-package"></a>测试第 2 课教程包  
  
1.  在 **“解决方案资源管理器”** 中，右键单击 **“Lesson 2.dtsx”** ，然后单击 **“执行包”**。  
  
    包将运行。 可以在“输出”窗口中或单击 **“进度”** 选项卡来验证每个循环的状态。例如，可以看到 1097 行从文件 Currency_VEB.txt 添加到目标表中。  
  
2.  当包运行完毕后，在 **“调试”** 菜单中，单击 **“停止调试”**。  
  
## <a name="next-lesson"></a>下一课  
[第 5 课：添加包部署模型的 SSIS 包配置](../integration-services/lesson-5-add-ssis-package-configurations-for-the-package-deployment-model.md)  
  
## <a name="see-also"></a>另请参阅  
[项目和包的执行](~/integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)  
  
  
  

