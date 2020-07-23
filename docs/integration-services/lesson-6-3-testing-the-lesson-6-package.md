---
title: 步骤 3：测试第 6 课包 | Microsoft Docs
ms.custom: ''
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: c184c92d-948f-4037-a502-5fabd909c84c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: dec02c9a17a2eb1db3411c9b359ad55a83ac4fa5
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/22/2020
ms.locfileid: "86922361"
---
# <a name="lesson-6-3-test-the-lesson-6-package"></a>第 6-3 课：测试第 6 课包

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


在运行时，包从 VarFolderName 参数获取 Directory 属性的值   。  
  
若要验证该包是否更新了 Directory 属性，只需执行该包即可  。 因为已将三个示例数据文件复制到新目录中，所以数据流会运行三次。
  
## <a name="check-the-package-layout"></a>检查包布局  
在测试包之前，请验证第 6 课包中的控件和数据流是否与下图中显示的对象类似：   
  
**控制流**  
  
![控制流](../integration-services/media/task4lesson2control.gif "控制流")  
  
**数据流**  
  
![数据流](../integration-services/media/task5lesson5data.gif "数据流")  
  
## <a name="test-the-lesson-6-package"></a>测试第 6 课包  
  
1.  在“调试”菜单中，选择“启动调试”   。  
  
2.  当包运行完毕后，在“调试”菜单中，选择“停止调试”   。  
  
## <a name="go-to-next-task"></a>转到下一个任务
[步骤 4：部署第 6 课包](../integration-services/lesson-6-4-deploying-the-lesson-6-package.md)  
  
  
  
