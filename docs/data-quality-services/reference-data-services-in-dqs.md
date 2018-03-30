---
title: DQS 中的 Reference Data Services | Microsoft Docs
ms.custom: ''
ms.date: 10/01/2012
ms.prod: sql-non-specified
ms.prod_service: data-quality-services
ms.service: ''
ms.component: data-quality-services
ms.reviewer: ''
ms.suite: sql
ms.technology:
- data-quality-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ef217717-6d05-443e-af26-44dc745a349d
caps.latest.revision: ''
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ee0c75c41ac8feb6141adbaa0ef1daa363b31d6f
ms.sourcegitcommit: 34766933e3832ca36181641db4493a0d2f4d05c6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2018
---
# <a name="reference-data-services-in-dqs"></a>DQS 中的 Reference Data Services
  引用数据指的是可信公共域或高级商业内容提供程序中提供的一组准确和完整的相关或分类全局数据（超越企业的界限）。  
  
 通过 [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] 中的“引用数据服务”功能，您可以订阅第三方引用数据提供程序，通过对照其高质量数据进行验证以轻松地清理和丰富您的业务数据。 您可以使用 DQS 内领先的数据质量服务提供程序的服务在清理过程中对数据执行标准化、更正数据或使数据更为丰富。 例如，您可以使用区号或邮政编码列表对照引用数据来验证您的客户的地址。  
  
 “引用数据服务”功能具有以下优点：  
  
-   借助引用数据，您可以通过将您的数据与第三方公司保证的数据进行比较来确保您数据的质量。  
  
-   引用数据过程合并到 DQS 知识库生成和数据质量项目中，这使您可以建立全面的数据质量过程。  
  
-   支持使用来自 Windows Azure Marketplace 的引用数据，以及直接来自第三方引用数据提供程序的引用数据。  
  
##  <a name="Marketplace"></a> 使用来自 Windows Azure Marketplace 的引用数据  
 DQS 支持使用来自 Windows Azure Marketplace 的引用数据，使内容提供程序能够通过 Marketplace 提供引用数据服务。 Marketplace 是 Microsoft 的一项服务，它为高质量数据和应用程序提供单一市场和交付渠道来作为云服务。 有关 Marketplace 的详细信息，请参阅 [了解 Microsoft Azure Marketplace](http://go.microsoft.com/fwlink/?LinkId=211291) (http://go.microsoft.com/fwlink/?LinkId=211291)。  
  
 Marketplace 和 DQS 之间的无缝集成简化了与从 DQS 中发现、浏览和获取数据质量项目的信息相关的步骤。 从 DQS 中使用数据，并通过使用一种创新方法将 DQS、Marketplace 和引用数据服务提供程序结合起来，帮助 DQS 用户获得高数据质量。  
  
 若要在 DQS 中使用来自 Marketplace 的引用数据执行清理活动，您必须具有 Marketplace 帐户密钥。 创建 Marketplace 帐户密钥是免费的，仅当您订阅付费数据集时才需要付费。 订阅和使用免费数据集都不需要付费。 有关创建 Marketplace 帐户密钥的详细信息，请参阅[创建帐户](http://go.microsoft.com/fwlink/?LinkId=212936) (http://go.microsoft.com/fwlink/?LinkId=212936)。  
  
 此外，还可以从 DQS 中执行以下 Marketplace 活动：  
  
-   浏览 Marketplace 中的数据集。  
  
-   创建 Marketplace 帐户密钥。  
  
-   管理您的 Marketplace 帐户详细信息，如针对数据提供程序的帐户密钥和订阅。  
  
 您可以在 **的** “配置” **屏幕的** “引用数据” [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]选项卡中执行这些活动。  
  
##  <a name="Direct"></a> 使用直接来自第三方引用数据提供程序的引用数据  
 如果您没有连接到 Internet 并因此无法使用 Marketplace，DQS 还支持直接连接到您组织的网络中提供的数据提供程序。 若要使用来自直接联机第三方引用数据提供程序的引用数据，您必须在 DQS 中为此数据提供程序创建一条记录。  
  
##  <a name="HowToCleanse"></a> 如何使用引用数据清理数据  
 在 DQS 中使用引用数据清理您的数据包括以下这些步骤：  
  
1.  **在 DQS 中配置引用数据提供程序详细信息**：您必须在 DQS 中配置引用数据服务详细信息，才能在 DQS 中使用引用数据。  
  
    1.  如果您正在使用 Marketplace，则提供一个有效的 Marketplace 帐户密钥，浏览至 Marketplace 中的 [Data Quality Services](http://go.microsoft.com/fwlink/?LinkId=227587) 数据类别，并订阅所需的提供程序。  
  
    2.  如果您正在使用直接联机引用数据提供程序，则在使用之前，必须在 DQS 中添加直接引用数据提供程序详细信息。  
  
     对于特定数据提供程序，在 DQS 中配置引用数据提供程序详细信息是一个一次性活动。 在 DQS 中，只有 DQS 管理员才能配置引用数据设置。  
  
2.  **将知识库中的域/复合域映射到引用数据服务**：将域/复合域映射到在步骤 1 中订阅/添加的相应引用数据服务。  
  
3.  **使用映射域在数据质量项目中进行清理活动**：在为 **“清理”** 活动创建数据质量项目时，选择包含在步骤 2 中映射到引用数据服务的域/复合域的知识库，然后执行清理活动。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|任务说明|主题|  
|----------------------|-----------|  
|介绍如何配置 DQS 以使用来自 Marketplace 或直接第三方联机数据提供程序的引用数据服务。|[将 DQS 配置为使用引用数据](../data-quality-services/configure-dqs-to-use-reference-data.md)|  
|介绍如何将知识库中的域/复合域映射到引用数据服务。|[将域或复合域附加到引用数据](../data-quality-services/attach-domain-or-composite-domain-to-reference-data.md)|  
|介绍如何使用引用数据服务清理数据。|[使用引用数据（外部）知识清理数据](../data-quality-services/cleanse-data-using-reference-data-external-knowledge.md)|  
  
  
