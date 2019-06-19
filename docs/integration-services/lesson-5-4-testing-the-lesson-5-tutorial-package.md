---
title: 步骤 4：测试第 5 课包 | Microsoft Docs
ms.custom: ''
ms.date: 01/08/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 5215b77d-c2ec-4b25-a3de-ca49ea197d74
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fc67c0a145b1ec32dc14cae8d56e538f14c2808e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65721540"
---
# <a name="lesson-5-4-test-the-lesson-5-package"></a>第 5-4 课：测试第 5 课包

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



在运行时，包从配置变量中而非创建包时指定的目录名称中获取 Directory 属性的值  。 该变量的值来自 SSISTutorial.dtsConfig XML 文件  。  
  
若要验证该包在运行时是否使用新值更新了 Directory 属性，请运行该包  。 因为新目录中只有三个示例数据文件，所以数据流会运行三次。  
  
## <a name="checking-the-package-layout"></a>检查包布局  
在测试包之前，请验证第 5 课包中的控件和数据流是否与下图中显示的对象类似：  
  
**控制流**  
  
![包中的控制流](../integration-services/media/task4lesson2control.gif "Control flow in package")  
  
**数据流**  
  
![包中的数据流](../integration-services/media/task9lesson1data.gif "Data flow in package")  
  
## <a name="test-the-lesson-5-package"></a>测试第 5 课包  
  
1.  在“调试”菜单中，选择“启动调试”   。  
  
2.  当包运行完毕后，在“调试”菜单中，选择“停止调试”   。  
  
## <a name="next-lesson"></a>下一课  
[第 6 课：在 SSIS 中对项目部署模型使用参数](../integration-services/lesson-6-using-parameters-with-the-project-deployment-model-in-ssis.md)  
  
  
  
