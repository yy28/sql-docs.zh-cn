---
title: 步骤 5：测试更新的包 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: tutorial
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- SQL Server 2016
ms.assetid: 683e52e5-1c7e-49ab-9ffe-6a450a1c5776
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 07da75fc6f7f703d5767b393ea662904dd6a1c36
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="lesson-1-5---testing-the-updated-packages"></a>第 1-5 课 - 测试更新的包
继续学习下一课（在该课中，您将创建用来在目标计算机上安装教程包的部署捆绑）之前，您应该测试包。 在此任务中，您将运行已添加到 Deployment Tutorial 项目中再用配置进行扩展的包 DataTransfer.dtsx 和 LoadXMLData。  
  
当包运行时，随着它成功完成，包中的每个可执行文件都将变为绿色。 当所有可执行文件都为绿色时，包已成功完成。 还可以在“进度”选项卡上查看包的执行进度。  
  
如果包未成功运行，则您必须先修复它们，再继续学习下一课。  
  
### <a name="to-run-the-datatransfer-package"></a>运行 DataTransfer 包  
  
1.  在解决方案资源管理器中，单击 DataTransfer.dtsx。  
  
2.  在 **“调试”** 菜单中，单击 **“启动调试”**。  
  
3.  当包运行完毕后，在 **“调试”** 菜单中，单击 **“停止调试”**。  
  
### <a name="to-run-the-loadxmldata-package"></a>运行 LoadXMLData 包  
  
1.  在解决方案资源管理器中，单击 LoadXMLData.dtsx。  
  
2.  在 **“调试”** 菜单中，单击 **“启动调试”**。  
  
3.  当包运行完毕后，在 **“调试”** 菜单中，单击 **“停止调试”**。  
  
## <a name="next-lesson"></a>下一课  
[第 2 课：在 SSIS 中创建部署捆绑](../integration-services/lesson-2-create-the-deployment-bundle-in-ssis.md)  
  
  
  
