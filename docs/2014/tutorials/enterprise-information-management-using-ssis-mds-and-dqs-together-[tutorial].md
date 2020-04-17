---
title: 将 SSIS、MDS 和 DQS 结合使用的企业信息管理 [教程] |微软文档
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
ms.openlocfilehash: 29ed5816a3a5fc0af6c5a4ac144557933e3e1a5f
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487716"
---
# <a name="enterprise-information-management-using-ssis-mds-and-dqs-together-tutorial"></a>综合使用 SSIS、MDS 和 DQS 来执行企业信息管理 [教程]
  在企业中管理信息通常涉及集成来自企业和企业之外的信息、清理数据、对数据进行匹配以便删除重复项、标准化数据、丰富数据、使数据符合法律和遵从性要求，以及将数据存储于具有所有必需的安全设置的集中位置。  
  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 在单个产品中提供一个有效企业信息管理 (EIM) 解决方案所需的所有组件。 可帮助您生成 EIM 解决方案的关键组件是：  
  
-   SQL Server Integration Services  
  
-   SQL Server Data Quality Services  
  
-   SQL Server Master Data Services  
  
 SQL Server Integration Services (SSIS) 提供强大的可扩展平台，用于在支持业务工作流、数据仓库或主数据管理的全面的提取、转换和加载 (ETL) 解决方案中集成来自不同源的数据。 有关 SSIS 的快速概述和典型用途，请参阅[集成服务概述](https://msdn.microsoft.com/library/ms141263\(SQL.105\).aspx)主题。  
  
 通过 SQL Server Data Quality Services (DQS)，您可以清理、匹配、标准化和丰富数据，以便您可以提供可信的信息来用于商业智能、数据仓库和事务处理工作负荷。 有关 DQS 的业务需求以及 DQS 如何满足需求，请参阅[介绍数据服务质量主题](https://msdn.microsoft.com/library/ff877917.aspx)。  
  
 SQL Server Master Data Services (MDS) 提供一个集中的数据中心，确保信息的完整性和数据的一致性在不同应用程序中是不变的。 有关 MDS 重要功能的简要说明，请参阅[主数据服务概述](../master-data-services/master-data-services-overview-mds.md)主题。  
  
 请参阅[使用 EIM 技术白皮书清理和匹配主数据](https://msdn.microsoft.com/library/hh403491.aspx)，了解有关使用这些 Microsoft EIM 技术实现 EIM 解决方案的全面指南，并观看[企业信息管理 （EIM）：将 SSIS、DQS 和 MDS 视频整合在一起](https://go.microsoft.com/fwlink/?LinkId=258672)，以便对 EIM 方案进行冷静演示。  
  
 在本教程中，您将学习如何一起使用 SSIS、MDS 和 DQS 来实现一个示例企业信息管理 (EIM) 解决方案。 首先，您将使用 DQS 创建一个包含与数据（元数据）有关的知识的知识库，通过使用该知识库清理一个 Excel 文件中的数据，并且对数据进行匹配以便标识并删除数据中的重复项。 接下来，您将使用用于 Excel 的 MDS 外接程序将已清理和匹配的数据上载到 MDS。 然后，您通过使用一个 SSIS 解决方案自动化整个过程。 本教程中的 SSIS 解决方案从 Excel 文件读取输入数据，但您可以将其扩展到从 Oracle、Teradata、DB2 和 Azure SQL 数据库等各种源读取。  
  
## <a name="prerequisites"></a>先决条件  
  
1.  安装了以下组件的 Microsoft SQL Server 2012。  
  
    1.  Integration Services (SSIS)  
  
    2.  Master Data Services (MDS)  
  
    3.  Data Quality Services (DQS)  
  
    4.  SQL Server Data Tools  
  
         有关安装产品的详细信息，请参阅[SQL Server 2012 安装指南](../database-engine/install-windows/installation-for-sql-server.md)。  
  
2.  [使用 Master Data Services 配置管理器配置 MDS](https://msdn.microsoft.com/library/ee633884.aspx)  
  
     使用配置管理器创建和配置 Master Data Services 数据库。 创建 MDS 数据库后，在 Web 站点中为 MDS 创建 Web`http://localhost/MDS`应用程序（例如： ），并将 MDS 数据库与 MDS Web 应用程序相关联。 请注意，若要创建 MDS Web 应用程序，您应该在您的计算机上安装有 IIS。 有关配置 MDS 数据库和 Web 应用程序的先决条件的详细信息，请参阅[Web 应用程序要求（主数据服务）](https://msdn.microsoft.com/library/ee633744.aspx)和[数据库要求（主数据服务）。](https://msdn.microsoft.com/library/ee633767.aspx)  
  
3.  [使用数据质量服务器安装程序安装和配置 DQS。](https://msdn.microsoft.com/library/hh231682.aspx) 单击 **"开始"，** 单击**所有程序**，单击**Microsoft SQL Server 2014**，单击**数据质量服务**，然后单击**数据质量服务器安装程序**。  
  
4.  Microsoft Excel 2010（首选 32 位）。  
  
5.  [从这里](https://www.microsoft.com/download/details.aspx?id=29064)安装**Excel 的主数据服务外接程序**（基于计算机上的 Excel 版本的 32 位或 64 位）。 要查找计算机上安装的 Excel 版本，请运行**Excel，** 单击菜单栏上的 **"文件**"，然后单击 **"帮助**"以查看右侧窗格中的版本。 请注意，您需要在安装 Excel 外接程序前安装 Visual Studio 2010 Tools for Office Runtime。  
  
6.  （可选）使用 Azure[应用商店](https://azuremarketplace.microsoft.com/marketplace/)创建帐户。 本教程中的一项任务要求您具有**Azure 应用商店**（最初称为**数据市场**）帐户。 如果需要您可以跳过此任务，继续执行下一任务。  
  
7.  从[微软下载中心](https://www.microsoft.com/download/details.aspx?id=50426)下载供应商.xls文件。  
  
8.  如果使用**64 位版本的 Excel**，则 DQS 不允许将清理结果或匹配结果导出到 Excel 文件。 此问题是一个已知问题。 若要解决此问题，请执行以下操作：  
  
    1.  运行**DQL 安装程序.exe -升级**。 如果您安装了 SQL Server 的默认实例，则 DQSInstaller.exe 文件将出现在 C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn 下。 双击 DQSInstaller.exe 文件。  
  
    2.  在**主数据服务配置管理器**中，单击 **"选择数据库**"，选择现有的**MDS**数据库，然后单击"**升级**"。  
  
## <a name="lessons"></a>课程  
  
|课程|简要描述|学完本课的估计时间（分钟）。|  
|------------|-----------------------|------------------------------------------------|  
|[第 1 课：创建 DQS Suppliers 知识库](../../2014/tutorials/lesson-1-creating-the-suppliers-dqs-knowledge-base.md)|在本课中，您将创建名为"**供应商"的**DQS 知识库。|60|  
|[第 2 课：使用 Suppliers 知识库清理供应商数据](../../2014/tutorials/lesson-2-cleansing-supplier-data-using-the-suppliers-knowledge-base.md)|在本课中，您将创建并运行一个 DQS 项目，通过使用您在第一课中创建的**供应商**知识库清理 Excel 文件中的供应商数据。|45|  
|[第 3 课：匹配数据以便从供应商列表中删除重复项](../../2014/tutorials/lesson-3-matching-data-to-remove-duplicates-from-supplier-list.md)|在本课中，您创建一个 DQS 项目以便执行匹配活动，从而从已清理的供应商列表中标识并删除重复项。|45|  
|[第 4 课：在 MDS 中存储供应商数据](../../2014/tutorials/lesson-4-storing-supplier-data-in-mds.md)|在本课中，您可以使用用于 Excel 的**MDS 外接程序**将清理和匹配的供应商数据上载到主数据服务 （MDS）。|45|  
|[第 5 课：使用 SSIS 自动执行清理和匹配](../../2014/tutorials/lesson-5-automating-the-cleansing-and-matching-using-ssis.md)|在本课中，您创建一个 SSIS 解决方案，该解决方案使用 DQS 清理输入数据、匹配已清理的数据以便删除重复项，以及以自动方式在 MDS 上存储已清理和匹配的数据。|75|  
  
## <a name="next-steps"></a>后续步骤  
 首先，请继续学习第一课：第[1 课：创建供应商 DQS 知识库](../../2014/tutorials/lesson-1-creating-the-suppliers-dqs-knowledge-base.md)。  
  
  
