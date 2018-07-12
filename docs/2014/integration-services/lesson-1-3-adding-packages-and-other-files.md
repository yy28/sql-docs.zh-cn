---
title: 步骤 3：添加包和其他文件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a7e6ec9c-d31d-4613-9525-8947a7b358f7
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4b2f66f8a8c5002d37948d110bd4b420c432d37b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37229307"
---
# <a name="step-3-adding-packages-and-other-files"></a>步骤 3：添加包和其他文件
  在此任务中，将现有的包、支持单个包的辅助文件以及自述文件添加到您在上一任务中创建的 Deployment Tutorial 项目。 例如，您将添加一个包含包数据的 XML 数据文件和一个提供有关项目中所有包的自述文件信息的文本文件。  
  
 在将包部署到测试环境或生产环境时，通常在部署中不包括数据文件，而是改用配置来更新数据源的路径，以访问数据文件或数据库的测试版本或生产版本。 为了便于学习，本教程将数据文件包括在包部署中。  
  
 在您安装 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 示例时，将安装包和包所用的示例数据。 将下列包添加到 Deployment Tutorial 项目：  
  
-   **DataTransfer。** 它是从平面文件提取数据、计算列值以便按条件保留数据集中的行、再将数据加载到 AdventureWorks 数据库中的表的基本包。  
  
-   **LoadXMLData。** 它是从 XML 数据文件提取数据、计算并聚合列值、再将数据加载到 AdventureWorks 数据库中的表的数据传输包。  
  
 若要支持这些包的部署，请将下列辅助文件添加到 Deployment Tutorial 项目。  
  
|“包”|文件|  
|-------------|----------|  
|DataTransfer|NewCustomers.txt|  
|LoadXMLData|orders.xml 和 orders.xsd|  
  
 还将添加一个自述文件，该文件是提供有关 Deployment Tutorial 项目的信息的文本文件。  
  
 在下列过程中使用的路径假定， [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 示例安装在默认位置 [!INCLUDE[ssSampPathIS](../includes/sssamppathis-md.md)]中。 如果将这些示例安装到其他位置，则应该使用该位置，而不是上述过程中的位置。  
  
 在下一任务中，将配置添加到 DataTransfer 和 LoadXMLData 包。 所有配置都存储在 XML 文件中，而且您将使用系统环境变量指定这些文件的位置。 创建配置文件后，将它们添加到项目。  
  
### <a name="to-add-packages-to-the-deployment-tutorial-project"></a>将包添加到 Deployment Tutorial 项目  
  
1.  如果 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 尚未打开，请单击“开始”，依次指向“所有程序”和“Microsoft SQL Server”，再单击“SQL Server Data Tools”。  
  
2.  在“文件”菜单上，依次单击“打开”、“项目/解决方案”、“Deployment Tutorial”文件夹，然后再次单击“打开”，最后双击“Deployment Tutorial.sln”。  
  
3.  在解决方案资源管理器中，右键单击“Deployment Tutorial”，再单击“添加”，然后单击“现有包”。  
  
4.  在“添加现有包的副本”对话框的“包位置”中，选择“文件系统”。  
  
5.  单击浏览 **(…)** 按钮，导航到 C:\Program Files\Microsoft SQL Server\100\Samples\Integration ServicesTutorial\Deploying Packages\Completed Packages，选择“DataTransfer.dtsx”，再单击“打开”。  
  
6.  单击“确定” 。  
  
7.  重复步骤 3-6，但这一次添加的是 LoadXMLData.dtsx（它位于 C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services\Tutorial\Deploying Packages\Completed Packages 中）。  
  
### <a name="to-add-ancillary-files-to-the-deployment-tutorial-project"></a>将辅助文件添加到 Deployment Tutorial 项目  
  
1.  在解决方案资源管理器中，右键单击“Deployment Tutorial”，再单击“添加”，然后单击“现有项”。  
  
2.  在“添加现有项 - Deployment Tutorial”对话框中，导航到 C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services\Tutorial\Deployment Packages\Sample Data，选择 orders.xml、orders.xsd 和 NewCustomers.txt，再单击“添加”。  
  
3.  在“添加现有项 - Deployment Tutorial”对话框中，导航到 C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services\Tutorial\Deployment Packages\\，选择 Readme.txt，再单击“添加”。  
  
4.  在“文件”菜单上，单击“全部保存”。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [步骤 4：添加包配置](../integration-services/lesson-1-4-adding-package-configurations.md)  
  
![集成服务图标 （小）](media/dts-16.gif "Integration Services 图标 （小）")**保持最新的 Integration Services** <br /> 若要从 Microsoft 获得最新的下载内容、文章、示例和视频，以及从社区获得所选解决方案，请访问 MSDN 上的 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 页：<br /><br /> [访问 MSDN 上的 Integration Services 页](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要获得有关这些更新的自动通知，请订阅该页上提供的 RSS 源。  
  
  
