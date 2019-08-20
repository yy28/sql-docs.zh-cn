---
title: SQL Server 隐私补充 | Microsoft Docs
ms.date: 01/19/2019
ms.prod: sql
ms.reviewer: mikeray
ms.custom: ''
ms.topic: conceptual
f1_keywords: ''
helpviewer_keywords: ''
author: aliceku
ms.author: aliceku
ms.openlocfilehash: c92eead00b10c4a26a93234c3bbfeebf254f6aff
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028846"
---
# <a name="sql-server-privacy-supplement"></a>SQL Server 隐私补充

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文总结了已启用 Internet 的功能，这些功能可收集并向 Microsoft 发送匿名功能使用情况和诊断数据。 SQL Server 可能会收集标准计算机信息，并可能会将有关使用情况和性能的数据传输给 Microsoft 进行分析，以便改进产品的质量、安全性和可靠性。 本文用作整个 [Microsoft 隐私声明](https://go.microsoft.com/fwlink/?LinkId=521839)的附录。 本文中的数据分类仅适用于 SQL Server 本地产品版本。 它不适用于：

- Azure SQL Database
- [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-telemetry-ssms?view=sql-server-2017)
- SQL Server Data Tools (SSDT)
- Azure Data Studio
- 数据库迁移助手
- SQL Server Migration Assistant
- MS-SQL 扩展

“允许的使用方案”定义  。 在本文的上下文中，Microsoft 将“允许的使用方案”定义为由 Microsoft 启动的操作或活动。

## <a name="access-control"></a>访问控制

使用凭据相关的信息在安装 SQL Server 期间对登录、用户或帐户进行保护。

### <a name="examples-of-access-control"></a>访问控制示例

- 密码
- 证书

### <a name="permitted-usage-scenarios"></a>允许的使用方案

|应用场景 |访问限制 |保留期要求 |
|---------|---------|---------|
|这些凭据通过使用情况和诊断数据始终保留在用户计算机上。 |- |- |
|故障转储可以包含访问控制数据。 |- |故障转储：最长 30 天。 |
|这些凭据通过用户反馈始终保留在用户计算机上（除非客户手动插入） |仅限 Microsoft 内部使用，不允许第三方访问。 |用户反馈：最长 1 年|
|&nbsp;|&nbsp;|&nbsp;|

## <a name="customer-content"></a>客户内容

根据定义，客户内容是指直接或间接存储在用户表中的数据。 该数据包括可能存储在用户表中的统计信息或查询文本中的用户文本。

### <a name="examples-of-customer-content"></a>客户内容示例

- 存储在任何用户表内各行中的数据值。
- 包含任何用户表内各行中值的副本的统计信息对象。
- 包含文本值的查询文本。

### <a name="permitted-usage-scenarios"></a>允许的使用方案

|应用场景  |访问限制  |保留期要求 |
|---------|---------|---------|
|此数据通过使用情况和诊断数据保留在用户计算机上。 |- |- |
|故障转储可以包含客户内容，并可以发送至 Microsoft。 |- |故障转储：最长 30 天。 |
|客户可自愿向 Microsoft 发送包含客户内容的用户反馈。 |仅限 Microsoft 内部使用，不允许第三方访问。 Microsoft 可向原始客户公开数据。 |用户反馈：最长 1 年 |

## <a name="end-user-identifiable-information-euii"></a>最终用户身份信息 (EUII)

从用户处接收的数据，或通过使用产品生成的数据。
- 对单个用户可链接。
- 不包含内容。

### <a name="examples-of-end-user-identifiable-information"></a>最终用户身份信息示例

- 接口标识。 完整的 IP 地址
- 计算机名称
- 登录名/用户名
- 电子邮件地址的本地部分 (joe@contoso.com)
- 位置信息
- 客户标识

### <a name="permitted-usage-scenarios"></a>允许的使用方案

|应用场景  |访问限制  |保留期要求|
|---------|---------|---------|
|此数据通过使用情况和诊断数据保留在用户计算机上。 |- |- |
|故障转储可包含 EUII，并可发送至 Microsoft。 |- |故障转储：最长 30 天 |
|客户标识 ID 可发送至 Microsoft，用于传递用户订阅的新混合和云功能。 |- |当前不提供此类混合或云功能。|
|客户可自愿向 Microsoft 发送包含客户内容的用户反馈。|仅限 Microsoft 内部使用，不允许第三方访问。 Microsoft 可向原始客户公开数据。 |用户反馈：最长 1 年 |

## <a name="internet-based-services-data"></a>基于 Internet 的服务数据

提供基于 Internet 的服务所需的数据（基于 SQL Server EULA）。

### <a name="examples-of-internet-based-services-data"></a>基于 Internet 的服务数据示例

- 计算机规范信息
- 浏览器名称/版本
- SQL Server 版本
- 语言代码
- 删除了特定八进制数的 IP 地址
- 地图数据

### <a name="permitted-usage-scenarios"></a>允许的使用方案

|应用场景  |访问限制  |保留期要求|
|---------|---------|---------| 
|Microsoft 可以使用该数据来优化功能和/或修复当前功能中的 bug。 |仅限 Microsoft 内部使用，不允许第三方访问。 Microsoft 可向原始客户公开数据。  例如，仪表板 |最短 90 天 - 最长 3 年 |
|客户可自愿向 Microsoft 发送包含客户内容的用户反馈。 |仅限 Microsoft 内部使用，不允许第三方访问。 |客户可自愿向 Microsoft 发送包含客户内容的用户反馈。 |
|Power View 和 SQL Server Reporting Services 地图项可发送数据供必应地图使用。 |仅限会话数据 |- |

## <a name="system-metadata"></a>系统元数据

运行服务器期间生成的数据。  该数据不包含客户内容。

### <a name="examples-of-system-metadata"></a>系统元数据示例

以下内容在不包含客户内容、对象元数据、客户访问控制数据或 EUII 时即被视为系统元数据：

- 数据库 GUID
- 计算机名称的哈希
- 实例名称的哈希
- 应用程序名称
- 行为/使用情况数据
- SQL 客户体验改善计划数据 (SQLCEIP)
- 服务器配置数据，例如 sp_configure 的设置
- 功能配置数据
- 事件名称和错误代码
- 硬件设置和 OEM 制造商等标识

Microsoft does 会检查由使用 SQL Server 的其他程序设置的应用程序名称值（示例：启用使用情况数据时，Sharepoint 或第三方打包程序在发送给 Microsoft 的系统元数据中包括此信息）。 客户不应将个人数据（如最终用户身份信息）存储在系统元数据字段中，也不应创建旨在将个人数据存储到这些字段的应用程序。 

### <a name="permitted-usage-scenarios"></a>允许的使用方案

|应用场景  |访问限制  |保留期要求|
|---------|---------|---------|
|Microsoft 可能使用它来优化功能，并/或修复当前功能中的 bug。|仅限 Microsoft 内部使用，不允许第三方访问。 |最短 90 天 - 最长 3 年 |
|可用于向客户提供建议。  例如，“根据产品的使用情况，建议使用功能 X，因为它性能更优良  。” |例如，Microsoft 可通过仪表板向原始客户公开该数据。 |客户数据安全日志：最短 3 年 - 最长 6 年 |
|Microsoft 可使用该数据对未来产品进行规划。 |Microsoft 可将此信息与其他硬件和软件供应商共享，以改善其产品在 Microsoft 软件中的运行性能。 |最短 90 天 - 最长 3 年|
|根据所发送的使用情况和诊断数据，Microsoft 可使用该数据来提供基于云的服务。 例如，显示组织中所有 SQL Server 安装的功能使用情况的客户仪表板。 |Microsoft 可通过仪表板向原始客户公开该数据。 |最短 90 天 - 最长 3 年 |
|客户可自愿向 Microsoft 发送包含客户内容的用户反馈。 |仅限 Microsoft 内部使用，不允许第三方访问。 Microsoft 可向原始客户公开数据。 |用户反馈：最长 1 年 |
|可使用数据库名称和应用程序名称将数据和应用程序归到已知的分类中，例如运行 Microsoft 提供的软件类别和运行其他公司提供的软件类别。|仅限 Microsoft 内部使用，不允许第三方访问。|最短 90 天 - 最长 3 年 |

## <a name="object-metadata"></a>对象元数据

本文中介绍的数据，或用于配置服务器、数据库、表和其他资源的数据。  对象元数据包括数据库表和列名称，但不包括数据库各行的内容或其他客户内容。 客户不应将个人数据（如最终用户身份信息）存储在对象元数据字段中，也不应创建旨在将个人数据存储到这些字段的应用程序。 对于以下允许的使用方案，只使用哈希格式来确定使用模式，从而改进产品。 

### <a name="examples-of-object-metadata"></a>对象元数据示例

- SQL Server 数据库名称
- 表名称和列名称
- 统计信息名称

### <a name="permitted-usage-scenarios"></a>允许的使用方案

> [!NOTE]
> 所有对象元数据值在收集之前都会经过哈希处理。
>

|应用场景  |访问限制  |保留期要求|
|---------|---------|---------|
|Microsoft 可能使用它来优化功能，并/或修复当前功能中的 bug。 |仅限 Microsoft 内部使用，不允许第三方访问。 |最短 90 天 - 最长 3 年|

## <a name="telemetry-controls"></a>遥测控件

若要了解如何在产品中打开/关闭遥测，请参阅此处的说明 - https://support.microsoft.com/help/3153756/how-to-configure-sql-server-2016-to-send-feedback-to-microsoft 。

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
