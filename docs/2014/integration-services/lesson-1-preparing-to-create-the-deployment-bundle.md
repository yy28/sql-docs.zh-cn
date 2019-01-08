---
title: 第 1 课：准备创建部署捆绑 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: b6fe283c-9856-4ba1-a497-e3912424fd18
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c4549800144012991b4d154eecb2f9bd67dee352
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/13/2018
ms.locfileid: "53364899"
---
# <a name="lesson-1-preparing-to-create-the-deployment-bundle"></a>第 1 课：准备创建部署捆绑
  在本课中，将创建支持教程的工作文件夹和环境变量，创建 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目，将几个包及其支持文件添加到项目，然后在包中实现配置。  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 基于项目部署包；因此，作为创建部署捆绑的第一步，必须将所有包和包依赖项集合到一个 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目中。 通常，包括已部署包的其他信息是很有用的：例如，您还将向项目中添加提供此组包的基本文档的自述文件。  
  
 添加包和文件后，将配置添加到尚未使用配置的包。 配置在运行时更新包和包对象的属性。 在后面的课程中，将在包部署期间修改这些配置的值，以便在部署到的环境中支持包。  
  
 添加配置后，应该在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器（用于生成 ETL 包的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 图形工具）中打开包，并检查包属性、包元素以及包配置，以便更好地了解部署需要解决的问题。 例如，其中一个包从文本文件提取数据，因此必须先更新数据文件的位置，已部署的包才能成功运行。  
  
 **估计的时间才能完成本课程中：** 1 小时  
  
## <a name="lesson-tasks"></a>课程任务  
 本课程包含以下任务：  
  
-   [第 1 步：创建工作文件夹和环境变量](../integration-services/lesson-1-1-creating-working-folders-and-environment-variables.md)  
  
-   [步骤 2:创建部署项目](../integration-services/lesson-1-2-creating-the-deployment-project.md)  
  
-   [步骤 3:添加包和其他文件](../integration-services/lesson-1-3-adding-packages-and-other-files.md)  
  
-   [步骤 4:添加包配置](../integration-services/lesson-1-4-adding-package-configurations.md)  
  
-   [步骤 5:测试更新的包](../integration-services/lesson-1-5-testing-the-updated-packages.md)  
  
## <a name="start-the-lesson"></a>开始课程  
 [第 1 步：创建工作文件夹和环境变量](../integration-services/lesson-1-1-creating-working-folders-and-environment-variables.md)  
  
![集成服务图标 （小）](media/dts-16.gif "Integration Services 图标 （小）")**保持最新的 Integration Services**<br /> 若要从 Microsoft 获得最新的下载内容、文章、示例和视频，以及从社区获得所选解决方案，请访问 MSDN 上的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 页：<br /><br /> [访问 MSDN 上的 Integration Services 页](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要获得有关这些更新的自动通知，请订阅该页上提供的 RSS 源。  
  
  
