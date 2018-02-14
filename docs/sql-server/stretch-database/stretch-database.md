---
title: Stretch Database | Microsoft Docs
ms.custom: 
ms.date: 06/27/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: stretch-database
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Stretch Database
ms.assetid: ce6db775-21a5-40bc-95a1-f560376d4ee2
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 30361d4466b7495945a7dae857bbcd52fd86103a
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="stretch-database"></a>Stretch Database
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


  Stretch Database 可以既透明又安全地将冷数据迁移到 Microsoft Azure 云。  
  
 如果你想立即开始使用 Stretch Database，请参阅 [Get started by running the Enable Database for Stretch Wizard](../../sql-server/stretch-database/get-started-by-running-the-enable-database-for-stretch-wizard.md)。  
  
## <a name="what-are-the-benefits-of-stretch-database"></a>Stretch Database 的优点是什么？  
 Stretch Database 具有下列优点：  
  
 **可以通过经济高效的方式来使用冷数据**  
 可以通过 SQL Server Stretch Database 以动态方式将冷、暖事务性数据从 SQL Server 延伸到 Microsoft Azure。 你的数据始终在线并可供查询使用，这与典型的冷数据存储不同。 你可以延长数据的保留时间，而不超出 Customer Order History 之类的大型表的限制。 充分利用 Azure 提供的低成本存储，不必进行昂贵的本地存储缩放。 你可以在 Azure 门户中选择定价层并配置设置，因此始终能够对价格和成本进行控制。 根据需要进行扩展或缩减。 有关详细信息，请访问 [SQL Server Stretch Database 定价](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/) 。  
  
 **不需更改查询或应用程序**  
 无缝访问 SQL Server 数据，不管这些数据是位于本地还是延伸到云中。  你设置决定数据存储位置的策略，而 SQL Server 则处理后台的数据移动。 整个表始终处于联机状态，始终可供查询。 而且，Stretch Database 不需对现有查询或应用程序进行任何更改 – 数据的位置对于应用程序来说是完全透明的。  
  
 **简化了本地数据维护过程**  
 降低了数据的本地维护和存储成本 对本地数据的备份运行速度更快，并在维护时段内完成。 自动运行对数据的云部分的备份。 你对本地存储的需求大大减少。 与增加本地 SSD 相比，Azure 存储空间的成本要便宜 80%。  
  
 **即使在迁移过程中，也会确保数据的安全性**  
 将你最重要的应用程序安全地延伸到云中，整个过程你都可以高枕无忧。 SQL Server 的始终加密功能为你的数据提供动态加密。 此外，还可以使用行级别安全性 (RLS) 和其他高级 SQL Server 安全功能以及 Stretch Database 来保护数据。  
  
## <a name="what-does-stretch-database-do"></a>Stretch Database 的功能是什么？  
 为 SQL 实例、数据库以及至少一个表启用 Stretch Database 以后，Stretch Database 就会开始以静默方式将你的冷数据迁移到 Azure。  
  
-   如果在单独的表中存储冷数据，则可以迁移整个表。  
  
-   如果表中同时包含热数据和冷数据，则可以指定筛选器函数以选择要迁移的行。

**不需更改现有查询和客户端应用。** 即使在数据迁移过程中，也可继续无缝访问本地数据和远程数据。 进行远程查询时，会有轻微滞后，但这种滞后只发生在查询冷数据时。

**Stretch Database 可以确保迁移过程中无数据丢失** （即使发生故障）。 它还可以通过重试逻辑来处理迁移过程中可能会发生的连接问题。 动态管理视图提供迁移的状态。

若要排查本地服务器上的问题，或最大限度地扩大可用网络带宽，**可暂停数据迁移** 。  
  
 ![Stretch Database 概述](../../sql-server/stretch-database/media/stretch-overview.png "Stretch Database 概述")  
  
## <a name="is-stretch-database-for-you"></a>Stretch Database 是否适合你？  
 如果你能够如实陈述以下情况，Stretch Database 也许能够帮助你满足相关要求并解决你的问题。  
  
|如果你是决策者|如果你是 DBA|  
|--------------------------------|---------------------|  
|我必须长期保留事务数据。|我的表的大小失去控制。|  
|有时候，我必须查询冷数据。|我的用户说他们想要访问冷数据，但只是偶尔使用。|  
|我安装了应用，包括较旧的应用，我不想对其进行更新。|我必须不断地购买和添加更多的存储。|  
|我想找到一种节省存储费用的方法。|我不能在 SLA 条件下备份或还原此类大型表。|  
  
## <a name="what-kind-of-databases-and-tables-are-candidates-for-stretch-database"></a>什么类型的数据库和表适用于 Stretch Database？  
 Stretch Database 针对的是包含大量冷数据的事务数据库，这些冷数据通常存储在少量表中。 这些表可能包含 10 亿多行。  
  
 如果你使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的临时表功能，则可使用 Stretch Database 将所有或部分关联的历史表迁移到 Azure 经济高效的存储中。 有关详细信息，请参阅 [管理版本由系统控制的临时表中历史数据的保留期](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)。  
  
 请使用 Stretch Database 顾问（SQL Server 2016 升级顾问的一项功能）来确定适用于 Stretch Database 的数据库和表。 有关详细信息，请参阅 [通过运行 Stretch Database 顾问标识适用于 Stretch Database 的数据库和表](../../sql-server/stretch-database/stretch-database-databases-and-tables-stretch-database-advisor.md)。 若要了解有关潜在阻滞问题的详细信息，请参阅 [Stretch Database 的局限性](../../sql-server/stretch-database/limitations-for-stretch-database.md)。  

## <a name="test-drive-stretch-database"></a>试用 Stretch Database  
 **通过 AdventureWorks 示例数据库试用 Stretch Database。** 若要获取 AdventureWorks 示例数据库，必须从 [此处](https://www.microsoft.com/en-us/download/details.aspx?id=49502)。 将示例数据库还原到 SQL Server 2016 实例后，请解压缩示例文件，然后从 Stretch DB 文件夹中打开 Stretch DB 示例文件。 运行此文件中的脚本来检查启用 Stretch Database 之前和之后数据使用的空间、跟踪数据迁移的进度，以及确认你是否可以继续在数据迁移期间和之后查询现有数据和插入新数据。  
  
## <a name="next-step"></a>下一步  
 **确定适用于 Stretch Database 的数据库和表。** 若要确定哪些数据库和表适用于 Stretch Database，请下载 SQL Server 2016 升级顾问并运行 Stretch Database 顾问。 Stretch Database 顾问也能标识阻止问题。 有关详细信息，请参阅 [通过运行 Stretch Database 顾问标识适用于 Stretch Database 的数据库和表](../../sql-server/stretch-database/stretch-database-databases-and-tables-stretch-database-advisor.md)。  
  
  
