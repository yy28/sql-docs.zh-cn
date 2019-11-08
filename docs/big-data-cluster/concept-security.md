---
title: 安全性概念
titleSuffix: SQL Server big data clusters
description: 本文介绍 SQL Server 大数据群集的安全性概念。 这包括介绍群集终结点和群集身份验证。
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 10/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 35eb5e0a3236d8f016ed5ca99b769d628a4d81ed
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/04/2019
ms.locfileid: "73532375"
---
# <a name="security-concepts-for-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 的安全性概念

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文将介绍大数据群集中与安全性相关的一些重要概念

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 提供连贯且一致的授权和身份验证。 大数据群集可通过完全自动化的部署与 Active Directory 进行集成，此部署可针对现有域设置 Active Directory 集成。 大数据群集配置了 Active Directory 集成后，你可以利用现有标识和用户组跨所有终结点进行统一访问。 此外，在 SQL Server 中创建外部表后，可通过向 Active Directory 用户和组授予对外部表的访问权限来控制对数据源的访问，从而将数据访问策略集中到一个位置。

## <a name="authentication"></a>身份验证

外部群集终结点支持 Active Directory 身份验证。 这意味着你可以使用 AD 标识对大数据群集进行身份验证。

### <a name="cluster-endpoints"></a>群集终结点

大数据群集有 5 个入口点

* 主实例 - 使用数据库工具和应用程序（如 SSMS 或 Azure Data Studio）访问群集中的 SQL Server 主实例所采用的 TDS 终结点。 从 azdata 中使用 HDFS 命令或 SQL Server 命令时，该工具将连接到其他终结点，具体取决于操作。

* 用于访问 HDFS 文件的网关 Spark (Knox) - 这是一个基于 HTTPS 的终结点。 此终结点用于访问 webHDFS 和 Spark 等服务。

* 群集管理服务（控制器）终结点 - 一种大数据群集管理服务，将公开用于管理群集的 REST API。 Azdata 工具需要连接到此终结点。

* 管理代理 - 用于访问“日志搜索”仪表板和“指标”仪表板。

* 应用程序代理 - 用于管理部署在大数据群集内部的应用程序的终结点。

![群集终结点](media/concept-security/cluster_endpoints.png)

目前没有打开其他端口以从外部访问群集的选项。

## <a name="authorization"></a>授权

在整个群集中，不同组件之间的集成安全性允许在从 Spark 和 SQL Server 中发出查询时，将原始用户的标识传递到 HDFS。 如上所述，各个外部群集终结点均支持 AD 身份验证。

群集中有两个级别的授权检查用于管理数据访问。 大数据上下文中的授权在 SQL Server 中完成，只需将对象上和 HDFS 中的传统 SQL Server 权限与访问控制列表 (ACL) 结合使用，将用户身份与特定权限相关联。

安全的大数据群集意味着跨 SQL Server 和 HDFS/Spark 对身份验证和授权方案提供一致的支持。 身份验证是指验证用户或服务身份并确保其与所声称的身份相符的过程。 授权是指基于发出请求的用户的身份，授予或拒绝对特定资源的访问权限。 此步骤在通过身份验证标识用户后执行。

大数据上下文中的授权通常通过访问控制列表 (ACL) 执行，后者将用户身份与特定权限相关联。 HDFS 通过限制对服务 API、HDFS 文件和作业执行的访问来支持授权。

## <a name="encryption-and-other-security-mechanisms"></a>加密和其他安全机制

客户端与外部终结点之间的通信加密以及群集内部组件之间的通信加密使用证书通过 TLS/SSL 获得保护。

所有 SQL Server 到 SQL Server 的通信（例如与数据池通信的 SQL 主实例）则通过 SQL 登录获得保护。

## <a name="basic-administrator-login"></a>基本管理员登录名

可选择在 Active Directory 模式下部署群集，或仅使用基本管理员登录名。 仅使用基本管理员登录名不是生产环境支持的安全模式，且主要用于评估产品。

即使选择 Active directory 模式，也会为群集管理员创建基本登录名。 如果 AD 连接关闭，这可以提供“后门”。

部署后，此基本登录名将被授予群集中的管理员权限。 这意味着用户将成为 SQL Server 主实例中的系统管理员以及群集控制器中的管理员。
Hadoop 组件不支持混合模式身份验证，这意味着不能使用基本管理员登录名对网关 (knox) 进行身份验证。


以下是在部署时需要定义的登录凭据。

群集管理员用户名：
 + `AZDATA_USERNAME=<username>`

群集管理员密码：  
 + `AZDATA_PASSWORD=<password>`

> [!NOTE]
> 请注意，在非 AD 模式下，必须将用户名“root”与上述密码结合使用，以便对网关 (Knox) 进行身份验证以访问 HDFS/Spark。

## <a name="next-steps"></a>后续步骤

若要了解有关 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 的详细信息，请参阅以下资源：

- [什么是 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]？](big-data-cluster-overview.md)
- [Workshop:Microsoft [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 体系结构](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
