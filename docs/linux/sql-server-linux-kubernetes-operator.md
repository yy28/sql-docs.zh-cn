---
title: SQL Server Always On 可用性组 Kubernetes 运算符全局要求
description: 本文介绍的 SQL Server Kubernetes Always On 可用性组运算符全局要求的参数
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: cd3cf1cd36866010843347d5c7a05a8cd39c20ef
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51660595"
---
# <a name="sql-server-always-on-availability-group-kubernetes-operator-parameters"></a>SQL Server Always On 可用性组 Kubernetes 运算符参数

Always On 可用性组在 Kubernetes 上的需要一个运算符。 清单说明运算符。 该清单是`.yaml`文件。 中的规范示例，请参阅[Always On 可用性组的 SQL Server 容器](sql-server-ag-kubernetes.md)。

本文介绍了运算符全局环境变量。

## <a name="example"></a>示例

下面的示例介绍如何以部署`mssql-operator`。

## <a name="global-environment-variables"></a>全局环境变量

* `MSSQL_K8S_POD_NAMESPACE` 
  * Required
  * **说明**： 运算符的 Kubernetes 命名空间。

* `MSSQL_K8S_SQL_WRITE_LEASE_PERIOD_SECONDS`
  * 可选
  * **说明**: sql server 写入租赁的持续时间。 使用保留的 sql server 可写并防止出现裂脑情况。 辅助副本等待此选择新领导后的秒数。

* `MSSQL_K8S_MONITOR_PERIOD_SECONDS`
  * 可选
  * **说明**： 要监视可用性组的状态的期间。 确定如何快速添加和删除副本。 必须是小于`MSSQL_K8S_SQL_WRITE_LEASE_PERIOD_SECONDS`。
  * **默认**: 1

* `MSSQL_K8S_LEASE_DURATION_SECONDS`
  * 可选
  * **说明**： 可用性组领导租约持续时间。 确定辅助副本重新选拔如果主副本已崩溃之前的等待多长时间。 这是不同于 SQL Server 写入租约。 
  * **默认**: 10
  
  >[!NOTE]
  >其他设置会自动计算基于`MSSQL_K8S_LEASE_DURATION_SECONDS`。

* `MSSQL_K8S_RENEW_DEADLINE_SECONDS`
  * 可选
  * **说明**： 充当主副本在放弃之前重试刷新领导的持续时间。 必须是小于`MSSQL_K8S_LEASE_DURATION_SECONDS`。
  * **默认值**:  `MSSQL_K8S_LEASE_DURATION_SECONDS` /2

* `MSSQL_K8S_RETRY_PERIOD_SECONDS`
  * 可选
  * **描述**： 持续时间生效[主](https://kubernetes.io/docs/concepts/architecture/master-node-communication/)续订领导租约之前等待。 必须是小于`MSSQL_K8S_LEASE_DURATION_SECONDS`。
  * **默认值**:  `MSSQL_K8S_RENEW_DEADLINE_SECONDS` /2

* `MSSQL_K8S_ACQUIRE_PERIOD_SECONDS` 
  * 可选
  * **说明**： 辅助副本轮询如果领导者租约已过期的时间。 
  * **默认**: 1


  ## <a name="next-steps"></a>后续步骤

[Kubernetes 群集上的 SQL Server 可用性组](sql-server-ag-kubernetes.md)
