---
title: 安全性概念
titleSuffix: SQL Server big data clusters
description: 本文介绍了 SQL Server 2019 大数据群集 （预览版） 的安全概念。 这包括描述群集终结点和群集身份验证。
author: nelgson
ms.author: negust
ms.reviewer: jroth
manager: jroth
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: d57fbeee578d2889d330ba19401477a43ab95e60
ms.sourcegitcommit: ce5770d8b91c18ba5ad031e1a96a657bde4cae55
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387944"
---
# <a name="security-concepts-for-sql-server-big-data-clusters"></a>SQL Server 大数据群集的安全性概念

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

安全的大数据群集在 SQL Server 和 HDFS/Spark 意味着统一且一致的身份验证和授权方案的支持。 身份验证是验证用户或服务的身份并确保它们它们声称自己谁的过程。 授权是指授予或拒绝对基于请求用户的标识的特定资源的访问。 用户标识通过身份验证后，执行此步骤。

通过访问控制列表 (Acl)，将用户标识与特定权限关联通常执行大数据上下文中的授权。 HDFS 支持通过限制对服务 Api、 HDFS 文件和作业执行的访问权限的授权。

本文将介绍在大数据群集中与安全相关的关键概念。

## <a name="cluster-endpoints"></a>群集终结点

有三个入口点到大数据群集

* 网关 HDFS/Spark (Knox)-这是一个基于 HTTPS 的终结点。 其他终结点是通过此代理。 HDFS/Spark 网关用于访问服务，如 webHDFS 和 Livy。 当你看到对 Knox 的引用，这是终结点。

* 控制器终结点-用于管理群集会公开 REST Api 的大数据群集管理服务。 某些工具还可以通过此终结点访问。

* 主实例的数据库工具和应用程序连接到 SQL Server 主实例在群集中的 TDS 端点。

![群集终结点](media/concept-security/cluster_endpoints.png)

目前，没有打开其他端口，用于从外部访问群集的选项。

### <a name="how-endpoints-are-secured"></a>如何保护终结点

完成保护大数据群集中的终结点使用密码可以是/更新集或者使用环境变量或 CLI 命令。 所有群集内部密码都存储为 Kubernetes 机密。  

## <a name="authentication"></a>身份验证

预配群集时将创建的登录名数。

这些登录名的一些服务相互通信，而有些则是为最终用户用于访问群集。

### <a name="end-user-authentication"></a>最终用户身份验证
在预配群集时需要使用环境变量进行设置的最终用户密码数。 以下是 SQL 管理员和群集管理员使用来访问服务的密码：

控制器用户名：
 + CONTROLLER_USERNAME=<controller_username>

控制器的密码：  
 + CONTROLLER_PASSWORD=<controller_password>

SQL 主控形状 SA 密码： 
 + MSSQL_SA_PASSWORD=<controller_sa_password>

用于访问 HDFS/Spark 终结点的密码：
 + KNOX_PASSWORD=<knox_password>

### <a name="intra-cluster-authentication"></a>群集内身份验证

时群集的部署，将创建的 SQL 登录名数：

* 由系统管理具有 sysadmin 角色的控制器 SQL 实例中创建的特殊 SQL 登录名。 此登录名的密码被捕获为 K8s 机密。

* 在群集中，控制器拥有并管理的所有 SQL 实例中创建的系统管理员登录名。 它是必需的控制器来执行管理任务，例如高可用性安装或升级，这些实例上。 这些登录名还用于 SQL 实例，如与数据池进行通信的 SQL 主控实例之间的群集内部通信。

> [!NOTE]
> 在当前版本中，支持仅基本身份验证。 精细的访问控制对 HDFS 对象和 SQL 大数据群集计算和数据池，尚不可用。

## <a name="intra-cluster-communication"></a>群集内部通信

使用证书保护与大数据群集，如 Livy Spark 或 Spark 到存储池内的非 SQL 服务的通信。 所有 SQL Server 到 SQL Server 的通信使用 SQL 登录名进行都保护。

## <a name="next-steps"></a>后续步骤

若要了解有关 SQL Server 大数据群集的详细信息，请参阅以下资源：

- [什么是 SQL Server 2019 大数据群集？](big-data-cluster-overview.md)
- [研讨会：Microsoft SQL Server 大数据群集体系结构](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)
