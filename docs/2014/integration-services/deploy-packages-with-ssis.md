---
title: SSIS 教程：部署包 |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- deployment tutorial [Integration Services]
- deploying packages [Integration Services]
- SSIS, tutorials
- Integration Services, tutorials
- deploying packages [Integration Services], installing
- SQL Server Integration Services, tutorials
- walkthroughs [Integration Services]
- deployment utility [Integration Services]
- deploying packages [Integration Services], configurations
ms.assetid: de18468c-cff3-48f4-99ec-6863610e5886
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3752c7e0f99a62534a670743c0ee7deb3c2e07a8
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58379715"
---
# <a name="ssis-tutorial-deploying-packages"></a>SSIS 教程：部署包
  [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 提供将包轻松部署到其他计算机的工具。 部署工具还管理任何依赖项，如包需要的配置和文件。 在本教程中，您将了解如何使用这些工具在目标计算机上安装包及其依赖项。  
  
 首先，您将执行任务为部署做好准备。 您将在 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中创建一个新的 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 项目，再将现有的包和数据文件添加到该项目。 不是从头开始创建任何新包，而是仅使用专为本教程创建的已完成包。 将不修改本教程中包的功能；但是，在将包添加到项目后，您可能会发现在 [!INCLUDE[ssIS](../includes/ssis-md.md)] 设计器中打开包并查看每个包的内容是很有用的。 通过检查包，您将了解有关包依赖项（如日志文件）的信息和有关包的其他有趣功能的信息。  
  
 在为部署做准备时，您还将更新包以使用配置。 配置使得包属性和包对象在运行时是可更新的。 在本教程中，您将使用配置来更新日志文件和文本文件的连接字符串以及包所用的 XML 和 XSD 文件的位置。 有关详细信息，请参阅 [包配置](../../2014/integration-services/package-configurations.md) 和 [创建包配置](../../2014/integration-services/create-package-configurations.md)。  
  
 在验证包是否在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]中成功运行后，将创建用来安装包的部署捆绑。 部署捆绑将包括包文件和您添加到 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目的其他项、 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 自动包括的包依赖项以及您生成的部署实用工具。 有关详细信息，请参阅 [Create a Deployment Utility](../../2014/integration-services/create-a-deployment-utility.md)。  
  
 然后，将部署捆绑复制到目标计算机，并运行包安装向导以安装包和包依赖项。 包将安装在 msdb SQL Server 数据库中，支持文件和辅助文件将安装在文件系统中。 由于已部署的包使用配置，因此将配置更新为使用新的值，这样包就可以在新环境中成功运行。  
  
 最后，通过使用执行包实用工具在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 中运行包。  
  
 本教程的目的是模拟实际部署中您可能遇到的问题的复杂性。 但是，如果不可能将包部署到其他计算机，仍可以学习本教程，方法是将包安装在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的本地实例上的 msdb 数据库中，再从同一实例上的 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 运行包。  
  
## <a name="what-you-will-learn"></a>学习内容  
 熟悉 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 中的新工具、控件和功能的最好方法，就是使用它们。 本教程将引导您完成创建 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目再将包和其他所需文件添加到项目的步骤。 完成项目后，将创建部署捆绑，将该捆绑复制到目标计算机，然后在目标计算机上安装包。  
  
## <a name="requirements"></a>要求  
 本教程适用于已经熟悉基本的文件系统操作，但对 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]中的新功能认识有限的用户。 若要更好地了解基本[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]将在本教程中使用的概念，你可能发现它可以先完成以下[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]教程：[运行 SQL Server 导入和导出向导](import-export-data/start-the-sql-server-import-and-export-wizard.md)和[SSIS 教程：创建简单的 ETL 包](../integration-services/ssis-how-to-create-an-etl-package.md)。  
  
 **源计算机** 将在其上创建部署捆绑的计算机必须安装下列组件：  
  
-   带有 AdventureWorks 数据库的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。 为了增强安全性，默认情况下不会安装示例数据库。 您可以下载示例数据库从[CodePlex](http://msftdbprodsamples.codeplex.com/releases/view/125550)。  
  
-   您必须具有在 AdventureWorks 中创建和删除表的权限。  
  
-   本教程还要求有示例数据、已完成的包、配置和自述文件。 这些项的文件与示例一起安装。 如果无法找到示例数据，请返回以上过程，按说明完成安装。  
  
-   商业智能开发环境 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]。  
  
 **目标计算机。** 向其部署程序包的计算机必须安装下列组件：  
  
-   带有 AdventureWorks 数据库的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]。  
  
-   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 的用户。  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]。  
  
-   必须具有在 AdventureWorks 中创建和删除表的权限以及在 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]中运行包的权限。  
  
-   您必须具有读取和写入权限在 msdb 中的 sysssispackages 表上[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]系统数据库。  
  
 如果您计划将包部署到在其上创建部署捆绑的计算机，则该计算机必须同时满足源计算机和目标计算机的要求。  
  
 **估计的时间才能完成本教程中：** 2 小时  
  
## <a name="lessons-in-this-tutorial"></a>本教程中的课程  
 [第 1 课：准备创建部署捆绑](../integration-services/lesson-1-preparing-to-create-the-deployment-bundle.md)  
 在本课中，将通过创建新的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 项目再将包和其他所需文件添加到该项目，为部署 ETL 解决方案做好准备。  
  
 [第 2 课：创建部署捆绑](../integration-services/lesson-2-create-the-deployment-bundle-in-ssis.md)  
 在本课中，将生成部署实用工具，并验证部署捆绑是否包括所需的文件。  
  
 [第 3 课：安装包](../integration-services/lesson-3-install-ssis-package.md)  
 在本课中，将部署捆绑复制到目标计算机，安装包，再运行包。  
  
![集成服务图标 （小）](media/dts-16.gif "Integration Services 图标 （小）")**保持最新的 Integration Services**<br /> 若要从 Microsoft 获得最新的下载内容、文章、示例和视频，以及从社区获得所选解决方案，请访问 MSDN 上的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 页：<br /><br /> [访问 MSDN 上的 Integration Services 页](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要获得有关这些更新的自动通知，请订阅该页上提供的 RSS 源。  
  
  
