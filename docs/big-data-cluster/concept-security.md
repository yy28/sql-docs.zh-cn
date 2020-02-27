---
title: 安全性概念
titleSuffix: SQL Server big data clusters
description: 本文介绍 SQL Server 大数据群集的安全性概念。 此内容包括对群集终结点和群集身份验证的介绍。
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 10/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 0fc816325d4008d1913f0e07e3032677a0eddb4d
ms.sourcegitcommit: 11691bfa8ec0dd6f14cc9cd3d1f62273f6eee885
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/07/2020
ms.locfileid: "77074415"
---
# <a name="security-concepts-for-big-data-clusters-2019"></a>[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 的安全性概念

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文将介绍大数据群集中与安全性相关的一些重要概念

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 提供连贯且一致的授权和身份验证。 大数据群集可通过对现有域设置 AD 集成的全自动化部署与 Active Directory (AD) 进行集成。 在大数据群集配置了 AD 集成后，你可以利用现有标识和用户组跨所有终结点进行统一访问。 此外，在 SQL Server 中创建外部表后，可通过向 AD 用户和组授予对外部表的访问权限来控制对数据源的访问，从而将数据访问策略集中到一个位置。

在这段 14 分钟的视频中，你将概览大数据群集的安全性：

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Overview-Big-Data-Cluster-Security/player?WT.mc_id=dataexposed-c9-niner]


## <a name="authentication"></a>身份验证

外部群集终结点支持 AD 身份验证。 使用 AD 标识对大数据群集进行身份验证。

### <a name="cluster-endpoints"></a>群集终结点

大数据群集有 5 个入口点

* 主实例 - 使用数据库工具和应用程序（如 SSMS 或 Azure Data Studio）访问群集中的 SQL Server 主实例所采用的 TDS 终结点。 从 azdata 中使用 HDFS 命令或 SQL Server 命令时，该工具将连接到其他终结点，具体取决于操作。

* 访问 HDFS 文件的网关 Spark (Knox) - 用于访问 webHDFS 和 Spark 等服务的 HTTPS 终结点。

* 群集管理服务（控制器）终结点 - 一种大数据群集管理服务，将公开用于管理群集的 REST API。 Azdata 工具需要连接到此终结点。

* 管理代理 - 用于访问“日志搜索”仪表板和“指标”仪表板。

* 应用程序代理 - 用于管理部署在大数据群集内部的应用程序的终结点。

![群集终结点](media/concept-security/cluster_endpoints.png)

目前没有打开其他端口以从外部访问群集的选项。

## <a name="authorization"></a>授权

在整个群集中，借助不同组件之间的集成安全性，可以在从 Spark 和 SQL Server 中发出查询时，将原始用户的标识一直传递到 HDFS。 如上所述，各个外部群集终结点均支持 AD 身份验证。

群集中有两个级别的授权检查用于管理数据访问。 大数据上下文中的授权在 SQL Server 中完成，只需将对象上和 HDFS 中的传统 SQL Server 权限与访问控制列表 (ACL) 结合使用，将用户身份与特定权限相关联。

安全的大数据群集意味着跨 SQL Server 和 HDFS/Spark 对身份验证和授权方案提供一致的支持。 身份验证是指验证用户或服务身份并确保其与所声称的身份相符的过程。 授权是指基于发出请求的用户的身份，授予或拒绝对特定资源的访问权限。 此步骤在通过身份验证标识用户后执行。

大数据上下文中的授权通常通过访问控制列表 (ACL) 执行，后者将用户身份与特定权限相关联。 HDFS 通过限制对服务 API、HDFS 文件和作业执行的访问来支持授权。

## <a name="encryption-and-other-security-mechanisms"></a>加密和其他安全机制

客户端与外部终结点之间的通信加密以及群集内部组件之间的通信加密使用证书通过 TLS/SSL 获得保护。

所有 SQL Server 到 SQL Server 的通信（例如与数据池通信的 SQL 主实例）则通过 SQL 登录获得保护。

> [!IMPORTANT]
>  大数据群集使用 etcd 来存储凭据。 最佳做法是确保将 Kubernetes 群集配置为在静态时使用 etcd 加密。 默认情况下，etcd 中存储的机密是未加密的。 Kubernetes 文档提供有关此管理任务的详细信息： https://kubernetes.io/docs/tasks/administer-cluster/kms-provider/ 和 https://kubernetes.io/docs/tasks/administer-cluster/encrypt-data/ 。


## <a name="basic-administrator-login"></a>基本管理员登录名

可选择在 AD 模式下部署群集，也可以只使用基本管理员登录。 只使用基本管理员登录不是生产支持的安全模式，旨在用于评估产品。

即使选择 Active directory 模式，也会为群集管理员创建基本登录名。 此功能提供了替代访问权限，以防 AD 连接断开。

部署后，此基本登录名将被授予群集中的管理员权限。 登录用户会成为 SQL Server 主实例中的系统管理员，以及群集控制器中的管理员。
Hadoop 组件不支持混合模式身份验证；也就是说，无法使用基本管理员登录对网关 (Knox) 进行身份验证。

部署期间需要定义的登录凭据包括：

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
