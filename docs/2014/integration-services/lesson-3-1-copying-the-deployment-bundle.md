---
title: 步骤 1：复制部署捆绑 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b6ef1e56-d278-4a24-afd3-68d8e0595cbb
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 1f8c86d77336ec9b8e17ddf9e4840a50f7a11b6a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36016877"
---
# <a name="step-1-copying-the-deployment-bundle"></a>步骤 1：复制部署捆绑
  在此任务中，将部署捆绑复制到目标计算机。  
  
 将部署捆绑复制到目标计算机的最简单方法是，首先在目标计算机上创建公共共享，将一个驱动器映射到公共共享，再将部署捆绑复制到该共享。 如何您不知道如何创建和配置公共文件夹或映射驱动器，请参阅 Windows 文档。  
  
### <a name="to-copy-the-deployment-bundle"></a>复制部署捆绑  
  
1.  在计算机上找到要复制的部署捆绑。  
  
     如果使用的是默认位置，则部署捆绑是 Deployment Tutorial 文件夹内的 Bin\Deployment 文件夹。  
  
2.  右键单击 Deployment 文件夹，再单击“复制”。  
  
3.  在目标计算机上找到要向其复制该文件夹的公共共享，再单击“粘贴”。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [步骤 2：运行包安装向导](../integration-services/lesson-3-2-running-the-package-installation-wizard.md)  
  
![集成服务图标 （小）](media/dts-16.gif "Integration Services 图标 （小）")**保持最新集成服务** <br /> 若要从 Microsoft 获得最新的下载内容、文章、示例和视频，以及从社区获得所选解决方案，请访问 MSDN 上的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 页：<br /><br /> [访问 MSDN 上的集成服务页](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要获得有关这些更新的自动通知，请订阅该页上提供的 RSS 源。  
  
  