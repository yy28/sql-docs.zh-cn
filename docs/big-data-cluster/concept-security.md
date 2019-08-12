---
title: 安全性概念
titleSuffix: SQL Server big data clusters
description: 本文介绍 SQL Server 2019 大数据群集（预览版）的安全性概念。 这包括介绍群集终结点和群集身份验证。
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 54ae86785590eb26fb8ac402f3ae8ab6c7f29a98
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/25/2019
ms.locfileid: "67958666"
---
# <a name="security-concepts-for-sql-server-big-data-clusters"></a>SQL Server 大数据群集的安全性概念

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

安全的大数据群集意味着跨 SQL Server 和 HDFS/Spark 对身份验证和授权方案提供一致的支持。 身份验证是指验证用户或服务身份并确保其与所声称的身份相符的过程。 授权是指基于发出请求的用户的身份，授予或拒绝对特定资源的访问权限。 此步骤在通过身份验证标识用户后执行。

大数据上下文中的授权通常通过访问控制列表 (ACL) 执行，后者将用户身份与特定权限相关联。 HDFS 通过限制对服务 API、HDFS 文件和作业执行的访问来支持授权。

本文将介绍大数据群集中与安全性相关的一些重要概念。

## <a name="cluster-endpoints"></a>群集终结点

大数据群集有三个入口点

* HDFS/Spark (Knox) 网关 - 这是一个基于 HTTPS 的终结点。 其他终结点通过它进行代理。 HDFS/Spark 网关用于访问 webHDFS 和 Livy 等服务。 无论在何处看到对 Knox 的引用，这都是终结点。

* 控制器终结点 - 一种大数据群集管理服务，将公开用于管理群集的 REST API。 还可以通过此终结点访问某些工具。

* 主实例 - 数据库工具和应用程序用于连接到群集中的 SQL Server 主实例的 TDS 终结点。

![群集终结点](media/concept-security/cluster_endpoints.png)

目前没有打开其他端口以从外部访问群集的选项。

### <a name="how-endpoints-are-secured"></a>如何保护终结点

使用可以通过环境变量或 CLI 命令设置/更新的密码来保护大数据群集中的终结点。 所有群集内部密码都存储为 Kubernetes 机密。  

## <a name="authentication"></a>身份验证

预配群集时，会创建许多登录名。

其中一些登录名用于服务之间的通信，另一些用于最终用户访问群集。

### <a name="end-user-authentication"></a>最终用户身份验证
预配群集时，需要使用环境变量设置许多最终用户密码。 这些是 SQL 管理员和群集管理员用来访问服务的密码：

控制器用户名：
 + CONTROLLER_USERNAME=<controller_username>

控制器密码：  
 + CONTROLLER_PASSWORD=<controller_password>

SQL 主 SA 密码： 
 + MSSQL_SA_PASSWORD=<controller_sa_password>

用于访问 HDFS/Spark 终结点的密码：
 + KNOX_PASSWORD=<knox_password>

### <a name="intra-cluster-authentication"></a>群集内身份验证

部署群集时，会创建许多 SQL 登录名：

* 在由系统管理的控制器 SQL 实例中创建一个具有 sysadmin 角色的特殊 SQL 登录名。 此登录名的密码被捕获为 K8s 机密。

* 在群集的所有 SQL 实例中创建一个 sysadmin 登录名，控制器拥有并管理该登录名。 控制器需要在这些实例上执行管理任务，例如 HA 设置或升级。 这些登录名还用于 SQL 实例之间的群集内通信，例如 SQL 主实例与数据池通信。

> [!NOTE]
> 在当前版本中，仅支持基本身份验证。 对 HDFS 对象以及 SQL 大数据群集计算和数据池的细化访问控制尚不可用。

## <a name="intra-cluster-communication"></a>群集内通信

使用证书保护与大数据群集内非 SQL 服务的通信（例如 Livy 到 Spark 或 Spark 到存储池）。 使用 SQL 登录名保护所有 SQL Server 到 SQL Server 的通信。

## <a name="next-steps"></a>后续步骤

若要了解有关 SQL Server 大数据群集的详细信息，请参阅以下资源：

- [什么是 SQL Server 2019 大数据群集？](big-data-cluster-overview.md)
- [Workshop:Microsoft SQL Server big data clusters Architecture](https://github.com/Microsoft/sqlworkshops/tree/master/sqlserver2019bigdataclusters)（研讨会：Microsoft SQL Server 大数据群集体系结构）
