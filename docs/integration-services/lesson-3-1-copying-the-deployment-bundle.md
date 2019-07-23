---
title: 第 1 步：复制部署捆绑 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: b6ef1e56-d278-4a24-afd3-68d8e0595cbb
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 6078f133e8f14f570540ff02a9f107578c5fada1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086530"
---
# <a name="lesson-3-1---copying-the-deployment-bundle"></a>第 3-1 课 - 复制部署捆绑

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


在此任务中，将部署捆绑复制到目标计算机。  
  
将部署捆绑复制到目标计算机的最简单方法是，首先在目标计算机上创建公共共享，将一个驱动器映射到公共共享，再将部署捆绑复制到该共享。 如何您不知道如何创建和配置公共文件夹或映射驱动器，请参阅 Windows 文档。  
  
### <a name="to-copy-the-deployment-bundle"></a>复制部署捆绑  
  
1.  在计算机上找到要复制的部署捆绑。  
  
    如果使用的是默认位置，则部署捆绑是 Deployment Tutorial 文件夹内的 Bin\Deployment 文件夹。  
  
2.  右键单击 Deployment 文件夹，再单击“复制”  。  
  
3.  在目标计算机上找到要向其复制该文件夹的公共共享，再单击“粘贴”  。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
[步骤 2：运行包安装向导](../integration-services/lesson-3-2-running-the-package-installation-wizard.md)  
  
  
  
