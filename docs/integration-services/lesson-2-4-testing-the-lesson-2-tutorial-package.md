---
title: 步骤 4：测试第 2 课教程包 | Microsoft Docs
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 0e8c0a25-8f79-41df-8ed2-f82a74b129cd
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7524010d42675b2eb503f8b8f43205a7ef2705b6
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2019
ms.locfileid: "58272211"
---
# <a name="lesson-2-4-test-the-lesson-2-tutorial-package"></a>第 2-4 课：测试第 2 课教程包

使用现在配置的 Foreach 循环容器和平面文件连接管理器，第 2 课包可以迭代遍历示例数据文件夹中的 14 个平面文件。 每次找到与指定的条件匹配的文件名时，Foreach 循环容器都将用该文件名填充用户定义的变量。 该变量又会更新平面文件连接管理器的 ConnectionString 属性，并与平面文件建立连接。 然后，Foreach 循环容器将对平面文件中的数据运行未修改的数据流任务。  
  
> [!NOTE]  
> 如果运行第 1 课中的包，则需要从 AdventureWorksDW2012 数据库中的 dbo.NewFactCurrencyRate 表中删除记录，然后再运行本课程中的包。 第 2 课尝试插入已在第 1 课中插入的记录，导致了错误。  
  
## <a name="check-the-package-layout"></a>检查包布局  
测试包之前，确保第 2 课包中的控制流和数据流包含下列关系图中显示的对象。 第 2 课的数据流和第 1 课一样。  
  
**控制流**  
  
![包中的控制流](../integration-services/media/task4lesson2control.gif "Control flow in package")  
  
**数据流**  
  
![包中的数据流](../integration-services/media/task9lesson1data.gif "Data flow in package")  
  
## <a name="test-the-lesson-2-tutorial-package"></a>测试第 2 课教程包  
  
1.  在“解决方案资源管理器”中，右键单击“Lesson 2.dtsx”，然后选择“执行包”。  
  
    包开始运行。 可以在“输出”窗口中或选择“进度”选项卡来验证每个循环的状态。例如，可以看到 1097 行从文件 Currency_VEB.txt 添加到目标表中。  
  
2.  当包运行完毕后，在“调试”菜单中，选择“停止调试”。  
  
## <a name="go-to-next-lesson"></a>转到下一课  
[第 3 课：使用 SSIS 添加日志记录](../integration-services/lesson-3-add-logging-with-ssis.md)  
  
## <a name="see-also"></a>另请参阅  
[项目和包的执行](../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)  
  
  
  

