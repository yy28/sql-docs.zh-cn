---
title: "第 3 课： 安装 SSIS 包 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: 87bc4d82-39d8-424f-886f-98cf1e4bb07a
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 986b8b46b7790b18442e17b6317f7816a0c7ec7c
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="lesson-3-install-ssis-packages"></a>第 3 课：安装 SSIS 包
在 [第 2 课：在 SSIS 中创建部署捆绑](../integration-services/lesson-2-create-the-deployment-bundle-in-ssis.md)中，生成了部署实用工具，并创建了包含必须在其他计算机上安装的各项的部署捆绑。 您还验证了部署捆绑中的文件列表，检查了在生成部署实用工具时创建的清单文件的内容。  
  
在本课中，将部署捆绑复制到目标计算机，然后在该计算机上运行包安装向导以安装包、包的依赖项和辅助文件。 包将安装在 **msdb**[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库中，其他项将安装在文件系统中。 完成包的安装后，将通过使用执行包实用工具从 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 运行包来测试部署。  
  
**学完本课的估计时间：** 30 分钟  
  
## <a name="lesson-tasks"></a>课程任务  
本课程包含以下任务：  
  
-   [步骤 1： 复制部署捆绑](../integration-services/lesson-3-1-copying-the-deployment-bundle.md)  
  
-   [步骤 2： 运行包安装向导](../integration-services/lesson-3-2-running-the-package-installation-wizard.md)  
  
-   [步骤 3： 测试已部署的包](../integration-services/lesson-3-3-testing-the-deployed-packages.md)  
  
## <a name="start-the-lesson"></a>开始课程  
[步骤 1：复制部署捆绑](../integration-services/lesson-3-1-copying-the-deployment-bundle.md)  
  
  
  

