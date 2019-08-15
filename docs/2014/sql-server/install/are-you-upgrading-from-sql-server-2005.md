---
title: 是否从 SQL Server 2005 进行升级？ | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 3d50a66a-1845-4116-8b3a-7b5a2eeb78e6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: aa1148d3c8b1031377cddd49c6a6c8698bafaf2e
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028524"
---
# <a name="are-you-upgrading-from-sql-server-2005"></a>是否从 SQL Server 2005 进行升级？
  需立即升级到较新版本的 SQL Server 和 Azure SQL 数据库的原因之一是，对 SQL Server 2005 的扩展支持已结束。 通过升级，你不仅可以维护安全性和合规性、获取突破性的性能，还可以优化你的数据平台基础结构。  
  
 有关计划和自动化你的升级或迁移的详细信息、指南和工具，请参阅 [SQL Server 2005 终止支持](https://www.microsoft.com/en-us/server-cloud/products/sql-server-2005/)。  
  
## <a name="why-upgrade"></a>升级理由  
  
> [!IMPORTANT]  
>  对于 SQL Server 2005 的延长支持将于 2016 年 4 月 12 日结束。 如果 2016 年 4 月 12 日后你仍在运行 SQL Server 2005，你将不会再收到安全更新。  
  
 若要获取有关从 SQL Server 2005 升级的 PDF 格式的产品介绍, 请[单击此处](https://info.microsoft.com/rs/157-GQE-382/images/EN-CNTNT-Infographic-UpgradeSQL2005Datasheet.pdf)(不是在下方的缩略图上)。  
  
 ![有关从 SQL Server 2005 升级的产品介绍](../../../2014/sql-server/install/media/sqlserver2005eos.png "有关从 SQL Server 2005 升级的产品介绍")  
  
## <a name="choose-your-upgrade-option"></a>选择升级选项  
 如果要从 SQL Server 2005 升级关系数据库, 以下是 Microsoft 平台上的关系存储的选项。  
  
 若要查看有关这些选项的更全面分析，请 [单击此处](http://sql05upgrade.azurewebsites.net/)。  
  
|关系存储选项|优势|要考虑的其他因素|  
|-------------------------------|--------------|-------------------------------|  
|**本地 SQL Server**<br /><br /> 对于任何类型的数据库应用程序（从交易系统到数据仓库），请考虑此选项。<br /><br /> 有关详细信息, 请参阅[SQL Server 2014](https://www.microsoft.com/EN-US/server-cloud/products/sql-server/)。|因为你管理硬件和软件，因此你对功能和可伸缩性具有最大控制权。<br /><br /> 如果是从 SQL Server 2005 升级, 则这是最相似的环境。|你必须做出最大的前期投资并进行日常管理，因为你需要购买、维护和管理你自己的硬件和软件。|  
|**Azure 虚拟机上托管的 SQL Server**<br /><br /> 如果你需要以下内容，请考虑此选项。<br />-迁移到托管环境的好处。<br />-控制操作环境。<br />-SQL Server 的熟悉功能集。<br /><br /> 有关详细信息, 请参阅[Azure 虚拟机上的 SQL Server 概述](https://azure.microsoft.com/documentation/articles/virtual-machines-sql-server-infrastructure-services/)。<br /><br /> 有关迁移的详细信息，请参阅 [将数据库迁移到 Azure VM 上的 SQL Server](https://azure.microsoft.com/documentation/articles/virtual-machines-migrate-onpremises-database/)。|可以从虚拟机映像库快速进行部署。<br /><br /> 获得完整的 SQL Server 功能集。<br /><br /> 节约硬件和服务器软件的成本。 只需支付每小时的使用费用。|必须配置并管理 SQL Server 和操作系统软件。|  
|**Azure SQL Database 托管的数据库服务**<br /><br /> 如果想要实现较少维护的低成本解决方案，请考虑此选项。<br /><br /> 此选项非常适用于不要求一直需要相同容量的应用，或必须提供外部访问的应用。<br /><br /> 有关详细信息, 请参阅[SQL 数据库](https://azure.microsoft.com/services/sql-database/)。<br /><br /> 有关迁移的信息, 请参阅将[SQL Server 数据库迁移到 AZURE SQL database](https://azure.microsoft.com/documentation/articles/sql-database-cloud-migrate/)。|可以快速部署并轻松纵向扩展。<br /><br /> 只需支付每小时的使用费用。<br /><br /> 该服务的成本不仅包括存储，还包括高可用性和自动执行的备份。|Azure SQL Database 缺少某些在托管的云环境中不适用的 SQL Server 功能。 有关详细信息，请参阅 [Azure SQL 数据库 Transact-SQL 信息](https://azure.microsoft.com/documentation/articles/sql-database-transact-sql-information/)。<br /><br /> 相较于 SQL Server 的 524 PB，Azure SQL Database 还具有 500 GB 的最大数据库大小。|  
  
 你还可能想要针对某些数据和应用程序考虑使用非关系或 NoSQL 解决方案。  
  
|非关系解决方案|优势|  
|------------------------------|--------------|  
|**Azure DocumentDB**<br /><br /> 对于现代、可伸缩、移动和 Web 应用程序（使用 JSON 数据并要求结合使用功能强大的查询和事务数据处理），请考虑此选项。<br /><br /> 有关详细信息，请参阅 [DocumentDB](https://azure.microsoft.com/services/documentdb/)。|已为你的文档编制索引，你可以使用熟悉的 SQL 语法来查询它们。<br /><br /> 该数据库未设计架构。<br /><br /> 无需重新生成索引即可向文档添加属性。<br /><br /> 直接在数据库引擎内获取 JSON 和 JavaScript 支持。<br /><br /> 获取对地理空间数据和集成其他 Azure 服务（包括 Azure Search、HDInsight 和 Data Factory）的本机支持。<br /><br /> 获得低延迟、高性能存储并保留吞吐量级别。|  
|**Azure 表存储**<br /><br /> 请考虑此选项以使用经济高效的解决方案存储数千兆半结构化数据。<br /><br /> 有关详细信息，请参阅 [表存储](https://azure.microsoft.com/services/storage/tables/)。|无需使数据离线即可扩展你的应用和表架构。<br /><br /> 无需分片数据集即可纵向扩展。<br /><br /> 获取跨多个区域复制数据的异地冗余存储。|  
  
 若要按照 Microsoft 上的说明下载报表“从 SQL Server 2005 进行迁移”（包含相关升级选项的详细信息），请 [单击此处](https://info.microsoft.com/CO-SQL-CNTNT-FY16-09Sep-14-ModernizationDirOnMFST-Register.html) （不是在下方的缩略图上）。  
  
 ![有关从 SQL Server 2005 迁移的报告](../../../2014/sql-server/install/media/sqlserver2005migratingdoc.png "有关从 SQL Server 2005 迁移的报告")  
  
## <a name="plan-your-upgrade"></a>规划升级  
  
-   阅读以下 SQL Server 团队博客文章系列中有关如何规划升级的内容。  
  
    -   [计划从 SQL Server 2005 进行高效升级:步骤 1 (共3步)](http://blogs.technet.com/b/dataplatforminsider/archive/2015/12/10/planning-an-efficient-upgrade-from-sql-server-2005-step-1-of-3.aspx)  
  
    -   [计划从 SQL Server 2005 进行高效升级:步骤 2 (共3步)](http://blogs.technet.com/b/dataplatforminsider/archive/2015/12/15/planning-an-efficient-upgrade-from-sql-server-2005-step-2-of-3.aspx)  
  
    -   [计划从 SQL Server 2005 进行高效升级:步骤 3 (共3步)](http://blogs.technet.com/b/dataplatforminsider/archive/2015/12/17/planning-an-efficient-upgrade-from-sql-server-2005-step-3-of-3.aspx)  
  
-   查看[规划 SQL Server 安装](../../../2014/sql-server/install/planning-a-sql-server-installation.md)所需的要求和注意事项, 包括[安装 SQL Server 2014 的硬件和软件要求](hardware-and-software-requirements-for-installing-sql-server.md)。  
  
-   阅读有关如何升级的内容。  
  
    -   查看 [Upgrade Database Engine](../../database-engine/install-windows/upgrade-database-engine.md)主题中的可用升级方法并了解规划和测试方法。  
  
        > [!IMPORTANT]  
        >  你不能就地将 SQL Server 2005 服务器升级到 SQL Server 2014。 你必须安装 Server 2014，然后将 SQL Server 2005 数据库迁移到新安装。  
  
    -   若要获取 PDF 格式的更详细的“技术升级指南”，请 [单击此处](https://download.microsoft.com/download/7/1/5/715BDFA7-51B6-4D7B-AF17-61E78C7E538F/SQL_Server_2014_Upgrade_technical_guide.pdf)。  
  
-   有关计划和自动化你的升级或迁移的详细信息、指南和工具，请参阅 [SQL Server 2005 终止支持](https://www.microsoft.com/en-us/server-cloud/products/sql-server-2005/)。  
  
## <a name="get-sql-server-2014"></a>获取 SQL Server 2014  
 若要下载 SQL Server 2014 的评估副本, 请[单击此处](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2014)。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 2014](https://www.microsoft.com/en-us/server-cloud/products/sql-server/default.aspx)   
 [SQL Server 2005 终止支持](https://www.microsoft.com/en-us/server-cloud/products/sql-server-2005/)   
 [从 SQL Server 2005 升级到 SQL Server 2016](https://msdn.microsoft.com/library/mt168847.aspx)  
  
  
