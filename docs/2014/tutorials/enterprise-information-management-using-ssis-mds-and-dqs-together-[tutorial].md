---
title: 使用 SSIS、MDS 和 DQS 结合使用企业信息管理 [教程] |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: ba09b504-3007-4cb7-8ef8-f01adbf51646
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 47bb74bf5fd35696481a88c4ccc30a8733f257a2
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2019
ms.locfileid: "70153564"
---
# <a name="enterprise-information-management-using-ssis-mds-and-dqs-together-tutorial"></a>综合使用 SSIS、MDS 和 DQS 来执行企业信息管理 [教程]
  在企业中管理信息通常涉及集成来自企业和企业之外的信息、清理数据、对数据进行匹配以便删除重复项、标准化数据、丰富数据、使数据符合法律和遵从性要求，以及将数据存储于具有所有必需的安全设置的集中位置。  
  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 在单个产品中提供一个有效企业信息管理 (EIM) 解决方案所需的所有组件。 可帮助您生成 EIM 解决方案的关键组件是：  
  
-   SQL Server Integration Services  
  
-   SQL Server Data Quality Services  
  
-   SQL Server Master Data Services  
  
 SQL Server Integration Services (SSIS) 提供强大的可扩展平台，用于在支持业务工作流、数据仓库或主数据管理的全面的提取、转换和加载 (ETL) 解决方案中集成来自不同源的数据。 有关 SSIS 的快速概述和典型用法, 请参阅[Integration Services 概述](https://msdn.microsoft.com/library/ms141263\(SQL.105\).aspx)主题。  
  
 通过 SQL Server Data Quality Services (DQS)，您可以清理、匹配、标准化和丰富数据，以便您可以提供可信的信息来用于商业智能、数据仓库和事务处理工作负荷。 请参阅[Data Quality Services 简介](https://msdn.microsoft.com/library/ff877917.aspx)主题, 了解 dqs 的业务需要以及 dqs 如何满足需要。  
  
 SQL Server Master Data Services (MDS) 提供一个集中的数据中心，确保信息的完整性和数据的一致性在不同应用程序中是不变的。 有关 MDS 的重要功能的简要说明, 请参阅[Master Data Services 概述](../master-data-services/master-data-services-overview-mds.md)主题。  
  
 有关使用这些 Microsoft EIM 技术实现 EIM 解决方案的全面指南, [请参阅[使用 EIM 技术清理和匹配主数据](https://msdn.microsoft.com/library/hh403491.aspx)。:将 SSIS、DQS 和 MDS](https://go.microsoft.com/fwlink/?LinkId=258672)视频组合在一起, 以提供 EIM 方案的酷演示。  
  
 在本教程中，您将学习如何一起使用 SSIS、MDS 和 DQS 来实现一个示例企业信息管理 (EIM) 解决方案。 首先，您将使用 DQS 创建一个包含与数据（元数据）有关的知识的知识库，通过使用该知识库清理一个 Excel 文件中的数据，并且对数据进行匹配以便标识并删除数据中的重复项。 接下来，您将使用用于 Excel 的 MDS 外接程序将已清理和匹配的数据上载到 MDS。 然后，您通过使用一个 SSIS 解决方案自动化整个过程。 本教程中的 SSIS 解决方案读取 Excel 文件中的输入数据, 但你可以将其扩展为从各种源 (如 Oracle、Teradata、DB2 和 Azure SQL 数据库) 读取数据。  
  
## <a name="prerequisites"></a>先决条件  
  
1.  安装了以下组件的 Microsoft SQL Server 2012。  
  
    1.  Integration Services (SSIS)  
  
    2.  Master Data Services (MDS)  
  
    3.  Data Quality Services (DQS)  
  
    4.  SQL Server Data Tools  
  
         有关安装该产品的详细信息, 请参阅[SQL Server 2012 安装指南](../database-engine/install-windows/installation-for-sql-server.md)。  
  
2.  [使用 Master Data Services 配置管理器配置 MDS](https://msdn.microsoft.com/library/ee633884.aspx)  
  
     使用配置管理器创建和配置 Master Data Services 数据库。 创建 mds 数据库后, 在网站中为 mds 创建一个 web 应用程序 (例如: [http://localhost/MDS](http://localhost/MDS)), 并将 mds 数据库与 mds web 应用程序相关联。 请注意，若要创建 MDS Web 应用程序，您应该在您的计算机上安装有 IIS。 有关配置 MDS 数据库和 Web 应用程序的先决条件的详细信息, 请参阅[Web 应用程序要求 (Master Data Services)](https://msdn.microsoft.com/library/ee633744.aspx)和[数据库要求 (Master Data Services)](https://msdn.microsoft.com/library/ee633767.aspx) 。  
  
3.  [使用数据质量服务器安装程序安装和配置 DQS](https://msdn.microsoft.com/library/hh231682.aspx)。 依次单击 "**开始**"、"**所有程序**"、 **Microsoft SQL Server 2014**、" **data Quality Services**", 然后单击 "**数据质量服务器安装程序**"。  
  
4.  Microsoft Excel 2010（首选 32 位）。  
  
5.  从[此处](https://www.microsoft.com/download/details.aspx?id=29064)安装**Master Data Services Add-in for Excel** (基于计算机上的 Excel 版本的32位或64位)。 若要查找计算机上安装的 Excel 版本, 请运行**excel**, 单击菜单栏上的 "**文件**", 然后单击 "**帮助**" 以在右窗格中查看该版本。 请注意, 在安装 Excel 外接程序之前, 需要安装 Visual Studio 2010 Tools for Office Runtime。  
  
6.  可有可无使用[Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/)创建帐户。 本教程中的任务之一要求你具有**Azure Marketplace** (最初称为 "**数据市场**") 帐户。 如果需要您可以跳过此任务，继续执行下一任务。  
  
7.  从[Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=50426)下载供应商 .xls 文件。  
  
8.  如果你使用**的是64位版本的 excel**, 则 DQS 不允许你将清理或匹配结果导出到 excel 文件中。 此问题是一个已知问题。 若要解决此问题，请执行以下操作：  
  
    1.  运行**DQLInstaller-upgrade**。 如果您安装了 SQL Server 的默认实例，则 DQSInstaller.exe 文件将出现在 C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn 下。 双击 DQSInstaller.exe 文件。  
  
    2.  在**Master Data Services 配置管理器**中, 单击 "**选择数据库**", 选择 "现有**MDS**数据库", 然后单击 "**升级**"。  
  
## <a name="lessons"></a>课程  
  
|课程|简要说明|学完本课的估计时间（分钟）。|  
|------------|-----------------------|------------------------------------------------|  
|[第 1 课：创建供应商 DQS 知识库](../../2014/tutorials/lesson-1-creating-the-suppliers-dqs-knowledge-base.md)|在本课中, 您将创建一个名为 "**供应商**" 的 DQS 知识库。|60|  
|[第 2 课：使用供应商知识库清理供应商数据](../../2014/tutorials/lesson-2-cleansing-supplier-data-using-the-suppliers-knowledge-base.md)|在本课中, 您将创建并运行一个 DQS 项目, 以便使用您在第一课中创建的**供应商**知识库来清理 Excel 文件中的供应商数据。|45|  
|[第 3 课：用于从供应商列表中删除重复项的匹配数据](../../2014/tutorials/lesson-3-matching-data-to-remove-duplicates-from-supplier-list.md)|在本课中，您创建一个 DQS 项目以便执行匹配活动，从而从已清理的供应商列表中标识并删除重复项。|45|  
|[第 4 课：在 MDS 中存储供应商数据](../../2014/tutorials/lesson-4-storing-supplier-data-in-mds.md)|在本课中, 您将使用**MDS Add-in for Excel**将清理和匹配的供应商数据上载到 MASTER DATA SERVICES (MDS)。|45|  
|[第 5 课：使用 SSIS 自动执行清理和匹配](../../2014/tutorials/lesson-5-automating-the-cleansing-and-matching-using-ssis.md)|在本课中，您创建一个 SSIS 解决方案，该解决方案使用 DQS 清理输入数据、匹配已清理的数据以便删除重复项，以及以自动方式在 MDS 上存储已清理和匹配的数据。|75|  
  
## <a name="next-steps"></a>后续步骤  
 若要开始学习本教程, 请继续学习第一课:[第 1 课：创建供应商 DQS 知识库](../../2014/tutorials/lesson-1-creating-the-suppliers-dqs-knowledge-base.md)。  
  
  
