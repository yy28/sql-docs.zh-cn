---
title: 企业信息管理使用 SSIS、 MDS 和一起 DQS [教程] |Microsoft 文档
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ba09b504-3007-4cb7-8ef8-f01adbf51646
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 1141b87ae8aadefdc72dba7e97a50649153a7b67
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36017447"
---
# <a name="enterprise-information-management-using-ssis-mds-and-dqs-together-tutorial"></a>综合使用 SSIS、MDS 和 DQS 来执行企业信息管理 [教程]
  在企业中管理信息通常涉及集成来自企业和企业之外的信息、清理数据、对数据进行匹配以便删除重复项、标准化数据、丰富数据、使数据符合法律和遵从性要求，以及将数据存储于具有所有必需的安全设置的集中位置。  
  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 在单个产品中提供一个有效企业信息管理 (EIM) 解决方案所需的所有组件。 可帮助您生成 EIM 解决方案的关键组件是：  
  
-   SQL Server Integration Services  
  
-   SQL Server Data Quality Services  
  
-   SQL Server Master Data Services  
  
 SQL Server Integration Services (SSIS) 提供强大的可扩展平台，用于在支持业务工作流、数据仓库或主数据管理的全面的提取、转换和加载 (ETL) 解决方案中集成来自不同源的数据。 请参阅[集成服务概述](http://msdn.microsoft.com/library/ms141263\(SQL.105\).aspx)来进行快速了解和典型的主题使用的 SSIS。  
  
 通过 SQL Server Data Quality Services (DQS)，您可以清理、匹配、标准化和丰富数据，以便您可以提供可信的信息来用于商业智能、数据仓库和事务处理工作负荷。 请参阅[简介 Data Quality Services](http://msdn.microsoft.com/library/ff877917.aspx)使 DQS 和 DQS 如何接听需要的业务需求的主题。  
  
 SQL Server Master Data Services (MDS) 提供一个集中的数据中心，确保信息的完整性和数据的一致性在不同应用程序中是不变的。 请参阅[Master Data Services Overview](http://msdn.microsoft.com/library/ff487003.aspx) MDS 的重要功能的简要说明的主题。  
  
 请参阅[清理和匹配主数据使用 EIM 技术](http://msdn.microsoft.com/library/hh403491.aspx)实现 EIM 解决方案结合使用这些 Microsoft EIM 技术及监视全面指导的白皮书[企业信息管理 (EIM): 将集合在一起 SSIS、 DQS 和 MDS](http://go.microsoft.com/fwlink/?LinkId=258672)有关 EIM 方案的冷演示视频。  
  
 在本教程中，您将学习如何一起使用 SSIS、MDS 和 DQS 来实现一个示例企业信息管理 (EIM) 解决方案。 首先，您将使用 DQS 创建一个包含与数据（元数据）有关的知识的知识库，通过使用该知识库清理一个 Excel 文件中的数据，并且对数据进行匹配以便标识并删除数据中的重复项。 接下来，您将使用用于 Excel 的 MDS 外接程序将已清理和匹配的数据上载到 MDS。 然后，您通过使用一个 SSIS 解决方案自动化整个过程。 本教程中的 SSIS 解决方案从一个 Excel 文件中读取输入数据，但您可以对其进行扩展，以便从不同数据源（例如 Oracle、Teradata、DB2 和 Windows Azure SQL Database）读取数据。  
  
## <a name="prerequisites"></a>必要條件  
  
1.  安装了以下组件的 Microsoft SQL Server 2012。  
  
    1.  Integration Services (SSIS)  
  
    2.  Master Data Services (MDS)  
  
    3.  Data Quality Services (DQS)  
  
    4.  SQL Server Data Tools  
  
         请参阅[SQL Server 2012 安装指南](http://msdn.microsoft.com/library/bb500469.aspx)有关安装产品的详细信息。  
  
2.  [配置 MDS 使用 Master Data Services 配置管理器](http://msdn.microsoft.com/library/ee633884.aspx)  
  
     使用配置管理器创建和配置 Master Data Services 数据库。 在创建 MDS 数据库后，请为 MDS 创建 web 应用程序，在网站 (例如： [ http://localhost/MDS ](http://localhost/MDS)) 并将 MDS 数据库与 MDS web 应用程序相关联。 请注意，若要创建 MDS Web 应用程序，您应该在您的计算机上安装有 IIS。 请参阅[Web 应用程序要求 (Master Data Services)](http://msdn.microsoft.com/library/ee633744.aspx)和[数据库要求 (Master Data Services)](http://msdn.microsoft.com/library/ee633767.aspx)有关配置 MDS 数据库和 web 应用程序的先决条件的详细信息。  
  
3.  [安装和使用数据质量服务器安装程序的配置的 DQS](http://msdn.microsoft.com/library/hh231682.aspx)。 单击**启动**，单击**所有程序**，单击**Microsoft SQL Server 2014**，单击**Data Quality Services**，然后单击**数据质量服务器安装程序**。  
  
4.  Microsoft Excel 2010（首选 32 位）。  
  
5.  安装**Master Data Services add-in for Excel** （32 位或 64 位基于你计算机具有的 Excel 版本） 从[此处](http://www.microsoft.com/download/details.aspx?id=29064)。 若要查找你的计算机上安装 Excel 的版本，请运行**Excel**，单击**文件**菜单栏，单击**帮助**若要查看在右窗格中的版本。 请注意，你需要安装 Visual Studio 2010 Tools for Office Runtime 安装 Excel 外接程序之前。  
  
6.  （可选）创建具有的帐户[Windows Azure 应用商店](https://datamarket.azure.com/)。 本教程中的任务之一要求你拥有**Azure 应用商店**(最初名为**数据市场**) 帐户。 如果需要您可以跳过此任务，继续执行下一任务。  
  
7.  下载 Suppliers.xls 文件[Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=271504)。  
  
8.  DQS 不允许您将清理或匹配结果保存到 Excel 文件，如果您使用导出**64 位版本的 Excel**。 此问题是一个已知问题。 若要解决此问题，请执行以下操作：  
  
    1.  运行**DQLInstaller.exe – 升级**。 如果您安装了 SQL Server 的默认实例，则 DQSInstaller.exe 文件将出现在 C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn 下。 双击 DQSInstaller.exe 文件。  
  
    2.  在**Master Data Services 配置管理器**，单击**选择数据库**，选择现有**MDS**数据库，并依次**升级**.  
  
## <a name="lessons"></a>课程  
  
|课程|简短说明|学完本课的估计时间（分钟）。|  
|------------|-----------------------|------------------------------------------------|  
|[第 1 课：创建 DQS Suppliers 知识库](../../2014/tutorials/lesson-1-creating-the-suppliers-dqs-knowledge-base.md)|在本课中，创建名为 DQS 知识库**供应商**。|60|  
|[第 2 课：使用 Suppliers 知识库清理供应商数据](../../2014/tutorials/lesson-2-cleansing-supplier-data-using-the-suppliers-knowledge-base.md)|在本课程中，创建并运行 DQS 项目，以通过使用清理 Excel 文件中的供应商数据**供应商**你在第一课中创建的知识库。|45|  
|[第 3 课：匹配数据以便从供应商列表中删除重复项](../../2014/tutorials/lesson-3-matching-data-to-remove-duplicates-from-supplier-list.md)|在本课中，您创建一个 DQS 项目以便执行匹配活动，从而从已清理的供应商列表中标识并删除重复项。|45|  
|[第 4 课：在 MDS 中存储供应商数据](../../2014/tutorials/lesson-4-storing-supplier-data-in-mds.md)|在本课程中，你已清理和匹配的供应商将数据上载到 Master Data Services (MDS) 通过使用**MDS add-in for Excel**。|45|  
|[第 5 课：使用 SSIS 自动执行清理和匹配](../../2014/tutorials/lesson-5-automating-the-cleansing-and-matching-using-ssis.md)|在本课中，您创建一个 SSIS 解决方案，该解决方案使用 DQS 清理输入数据、匹配已清理的数据以便删除重复项，以及以自动方式在 MDS 上存储已清理和匹配的数据。|75|  
  
## <a name="next-steps"></a>后续步骤  
 若要开始使用本教程，继续第一课：[第 1 课： 创建供应商 DQS 知识库](../../2014/tutorials/lesson-1-creating-the-suppliers-dqs-knowledge-base.md)。  
  
  