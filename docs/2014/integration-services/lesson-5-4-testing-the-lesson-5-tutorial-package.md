---
title: 步骤 4：测试第 5 课教程包 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5215b77d-c2ec-4b25-a3de-ca49ea197d74
author: janinezhang
ms.author: janinez
ms.openlocfilehash: e3bb87bbf5e3e17f5468fabe50c158b30239777d
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84951487"
---
# <a name="step-4-testing-the-lesson-5-tutorial-package"></a>步骤 4：测试第 5 课教程包
  在运行时，包从运行时更新的变量中获取 `Directory` 属性的值，而不是使用在创建包时指定的原始目录名。 该变量的值由 SSISTutorial.dtsConfig 文件填充。  
  
 若要验证该包在运行时是否使用新值更新了 Directory 属性，只需执行该包。 由于只向新目录中复制了三个示例数据文件，因此该数据流将只运行三次，而不遍历原始文件夹中的 14 个文件。  
  
## <a name="checking-the-package-layout"></a>检查包布局  
 测试程序包之前，应确保第 5 课包中的控制流和数据流包含显示在下列关系图中的对象。 控制流应与第 4 课中的控制流相同。 数据流应与第 4 课中的数据流相同。  
  
 **控制流**  
  
 ![包中的控制流](../../2014/tutorials/media/task4lesson2control.gif "包中的控制流")  
  
 数据流  
  
 ![包中的数据流](../../2014/tutorials/media/task9lesson1data.gif "包中的数据流")  
  
### <a name="to-test-the-lesson-5-tutorial-package"></a>测试 Lesson 5 教程包  
  
1.  在“调试”菜单上，单击“启动调试”。  
  
2.  包完成运行后，在 "**调试**" 菜单上，然后单击 "**停止调试**"。  
  
## <a name="next-lesson"></a>下一课  
 [第 6 课：对项目部署模型使用参数](../integration-services/lesson-6-using-parameters-with-the-project-deployment-model-in-ssis.md)  
  
  
