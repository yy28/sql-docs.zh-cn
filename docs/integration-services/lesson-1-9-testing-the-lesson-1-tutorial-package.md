---
title: 步骤 9：测试第 1 课教程包 | Microsoft Docs
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 9aee7acf-797b-46f2-830d-80ab64a9f0b6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a16deda0b17a15d6eae3c1e2b22e35b3fa8a9a7a
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2019
ms.locfileid: "58289763"
---
# <a name="lesson-1-9-test-the-lesson-1-package"></a>第 1-9 课：测试第 1 课包

在本教程中，已完成以下任务：  
  
-   创建了一个新的 [!INCLUDE[ssIS](../includes/ssis-md.md)] 项目。  
  
-   配置了包连接到源数据和目标数据的连接管理器。  
  
-   添加了一个数据流，该数据流从平面文件源提取数据，对数据执行必要的查找转换，并为目标配置数据。  
  
包现在已完成并可供测试！
  
## <a name="check-the-package-components"></a>检查包组件
  
测试包之前，确保第1 课包中的控制流和数据流包含下列关系图中显示的对象。  
  
**控制流** 
  
![包中的控制流](../integration-services/media/task9lesson1control.gif "Control flow in package")  
  
**数据流**  
  
![包中的数据流](../integration-services/media/task9lesson1data.gif "Data flow in package")  
  
## <a name="run-the-lesson-1-package"></a>运行第 1 课包  
  
1.  在“调试”菜单中，选择“启动调试”。  
  
    包开始运行，结果有 1097 行被成功添加到 AdventureWorksDW2012 中的 NewFactCurrencyRate 事实数据表中。 若要验证此结果，请选择“数据流”选项卡。
  
2.  当包运行完毕后，在“调试”菜单中，选择“停止调试”。  
  
## <a name="go-to-next-lesson"></a>转到下一课
[第 2 课：使用 SSIS 添加循环](../integration-services/lesson-2-adding-looping-with-ssis.md)  
  
## <a name="see-also"></a>另请参阅  
[项目和包的执行](packages/run-integration-services-ssis-packages.md) 
  
  
  
