---
title: 支持的版本和版本升级 | Microsoft Docs
ms.custom: ''
ms.date: 10/26/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- components [SQL Server], adding to existing installations
- versions [SQL Server], upgrading
- upgrading SQL Server, upgrades supported
- cross-language support
ms.assetid: 702359c4-6ca9-42a8-860c-a95a802898a1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4a245aab71292e1482bd5a17bd32a27bded640ab
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62775214"
---
# <a name="supported-version-and-edition-upgrades"></a>支持的版本和版本升级
  您可以从 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]和 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]进行升级。 本主题列出了支持的从这些 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本进行升级的途径以及支持的 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]版本升级。  
  
## <a name="pre-upgrade-checklist"></a>升级前的清单  
  
-   在从 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 的某个版本升级到另一个版本之前，请确认您当前所用的功能在要移到的版本中受支持。  
  
-   升级到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]之前，请先为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 启用 Windows 身份验证，并验证默认配置： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服务帐户是否是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sysadmin 组的成员。  
  
-   若要升级到 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]，您运行的必须是受支持的操作系统。 有关详细信息，请参阅 [Hardware and Software Requirements for Installing SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)。  
  
-   如果有挂起的重新启动操作，则会阻止升级。  
  
-   如果未运行 Windows Installer 服务，则会阻止升级。  
  
## <a name="unsupported-scenarios"></a>不受支持的方案  
  
-   不支持 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 的跨版本实例。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]、 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]和 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 组件的版本号在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]实例中必须相同。  
  
-   不支持跨平台升级。 不能使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 32 位实例升级到本机 64 位。 但是，如果数据库未在复制过程中发布，则可以从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的 32 位实例中备份或分离数据库，然后再将它们还原或附加到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的新实例（64 位）。 必须在 master、msdb 和 model 系统数据库中重新创建任何登录名和其他用户对象。  
  
-   不能在升级现有的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的过程中添加新功能。 将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 之后，您可以使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 安装程序添加功能。 有关详细信息，请参阅[添加到 SQL Server 2014 实例的功能&#40;安装程序&#41;](add-features-to-an-instance-of-sql-server-setup.md)。  
  
-   在 WOW 模式下不支持故障转移群集。  
  
-   不支持从以前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本的 Evaluation 版升级。  
  
## <a name="upgrades-from-earlier-versions-to-includesssql14includessssql14-mdmd"></a>从早期版本升级到 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
> [!NOTE]  
>  下一节“针对 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 的[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 支持”中更加详细地介绍了针对 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]的支持。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 32 位版本可在 64 位服务器的 32 位子系统 (WOW64) 上升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 64 位版本只能升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 64 位服务器。  
  
> [!NOTE]  
>  当你升级到[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]从以前版本的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Enterprise edition 中，Enterprise Edition 之间进行选择：基于内核的许可和企业版。 这些 Enterprise 版仅在许可模式和支持的内核的最大数目方面存在差异。 有关详细信息，请参阅 [Compute Capacity Limits by Edition of SQL Server](../../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)。  
  
 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 支持从以下版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进行升级：  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 或更高版本  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 或更高版本  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 或更高版本  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 或更高版本  
  
 下表列出了从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的早期版本升级到 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 的支持方案。  
  
|升级前的版本|支持的升级途径|  
|------------------|----------------------------|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 Enterprise|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 Developer|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Developer|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 Standard|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 Workgroup|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 Express、<br /><br /> [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 Express with Tools 和<br /><br /> [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 Express with Advanced Services|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Enterprise|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Developer|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Developer|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Standard|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Small Business|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Web|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Workgroup|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Express、<br /><br /> [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Express with Tools 和<br /><br /> [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Express with Advanced Services|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Datacenter|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Enterprise|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Developer|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Developer|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Small Business|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Standard|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Web|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Workgroup|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Express、<br /><br /> [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Express with Tools 和<br /><br /> [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Express with Advanced Services|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Enterprise|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Developer|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Developer|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Standard|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Web|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Express、<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Express with Tools 和<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Express Management Studio 和<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Express with Advanced Services|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Business Intelligence|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|  
  
### <a name="includesssql14includessssql14-mdmd-support-for-includessversion2005includesssversion2005-mdmd"></a>对 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 的 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 支持  
 此节讨论针对 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 的 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]支持。 在 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]中，您能够执行以下操作：  
  
-   通过使用安装向导或从命令提示符运行 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 安装程序，将数据库引擎的 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 实例升级到 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 。  
  
-   将 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 数据库（mdf/ldf 文件）附加到数据库引擎的 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 实例。  
  
-   从备份将 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 数据库还原为数据库引擎的 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 实例。  
  
-   将 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] 升级到 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]。 通过自动就地升级执行包。  
  
-   通过运行 [!INCLUDE[ssASversion2005](../../includes/ssasversion2005-md.md)] 安装程序，将 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 升级到 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 。  
  
-   备份 [!INCLUDE[ssASversion2005](../../includes/ssasversion2005-md.md)] 多维数据集并在 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]上还原。  
  
-   通过运行 [!INCLUDE[ssRSversion2005](../../includes/ssrsversion2005-md.md)] 安装程序，将 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 升级到 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 。  
  
-   使用 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]2014 连接到 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 。  
  
 当 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 数据库升级到 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 时，该数据库兼容级别将从 90 更改为 100。 (在[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]，数据库兼容性级别的有效值为 100、 110 和 120。)[ALTER DATABASE 兼容级别 (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level) 讨论兼容级别更改可能会影响 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 应用程序的方式。  
  
 不支持以上列表中未指定的任何方案，包括但不限于以下情况：  
  
-   在相同计算机上安装 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]（并行）。  
  
-   使用 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 实例作为涉及 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 实例的复制拓扑的成员。  
  
-   在 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 与 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 实例之间配置数据库镜像。  
  
-   使用日志传送在 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 与 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 实例之间备份事务日志。  
  
-   在 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 与 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 实例之间配置链接服务器。  
  
-   从 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Management Studio 管理 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 实例。  
  
-   在 [!INCLUDE[ssASversion2005](../../includes/ssasversion2005-md.md)] Management Studio 中附加 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 多维数据集。  
  
-   从 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] Management Studio 连接到 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 。  
  
-   从 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] Management Studio 管理 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 服务。  
  
-   支持 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 第三方自定义 Integration Services 组件，如执行和升级。  
  
## <a name="includesssql14includessssql14-mdmd-edition-upgrade"></a>[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 版本升级  
 下表列出了 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]中支持的版本升级方案。  
  
 有关如何执行版本升级的分步说明，请参阅[升级到不同版本的 SQL Server 2014&#40;安装程序&#41;](upgrade-to-a-different-edition-of-sql-server-setup.md)。  
  
|升级前的版本|升级到的版本|  
|------------------|----------------|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise （服务器 + CAL 和内核） <sup>2</sup>|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise（服务器+CAL 或内核许可证）|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 评估企业<sup>2</sup>|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise（服务器+CAL 或内核许可证）<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Developer<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web<br /><br /> 对于独立安装，支持从 Evaluation Enterprise（免费版本）升级到任何付费版本；但对于群集安装，则不支持此升级。|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 标准<sup>2</sup>|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise（服务器+CAL 或内核许可证）|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 开发人员<sup>2</sup>|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise（服务器+CAL 或内核许可证）<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise（服务器+CAL 或内核许可证）<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express <sup>1</sup>|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise（服务器+CAL 或内核许可证）<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Developer<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web|  
  
 此外，您还可以执行 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise（服务器+CAL 或内核许可证）和 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise（内核许可证）之间的版本升级：  
  
|版本升级自|版本升级到|  
|--------------------------|------------------------|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise （服务器 + CAL 许可证） <sup>2</sup>|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise（内核许可证）|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise（内核许可证）|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise（服务器+CAL 许可证）|  
  
 <sup>1</sup>也适用于[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]Express with Tools 和[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]Express with Advanced Services。  
  
 <sup>2</sup>版本的更改[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]故障转移群集是有限。 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 故障转移群集不支持以下方案：  
  
-   SQL Server 2014 Enterprise 到 SQL Server 2014 Developer、Standard 或 Enterprise Evaluation。  
  
-   SQL Server 2014 Developer 到 SQL Server 2014 Standard 或 Enterprise Evaluation。  
  
-   SQL Server 2014 Standard 到 SQL Server 2014 Enterprise Evaluation。  
  
-   SQL Server 2014 Enterprise Evaluation 到 SQL Server 2014 Standard。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 2014 的版本支持的功能](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [硬件和软件要求安装 SQL Server 2014 的](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)   
 [升级到 SQL Server 2014](upgrade-sql-server.md)   
 [使用升级顾问来准备升级](../../../2014/sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)  
  
  
