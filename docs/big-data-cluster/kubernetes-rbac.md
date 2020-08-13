---
title: Kubernetes RBAC
titleSuffix: SQL Server big data clusters
description: 本文介绍 SQL Server 大数据群集如何将 RBAC 与 Kubernetes 配合使用。
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 06/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5d2e3f379402f16f32020f9cd34103919f13a30c
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/21/2020
ms.locfileid: "86552972"
---
# <a name="kubernetes-rbac-model--impact-on-users-managing-bdc"></a>Kubernetes RBAC 模型及对用户管理 BDC 的影响

以下部分介绍了用户管理大数据群集所需的权限。

> [!NOTE]
> 有关 Kubernetes RBAC 模型的其他资源，请参阅[使用 RBAC 授权 - Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/rbac/) 及[使用 RBAC 定义和应用权限 - OpenShift](https://docs.openshift.com/container-platform/4.4/authentication/using-rbac.html)。

## <a name="role-required-for-deployment"></a>部署所需的角色

BDC 使用服务帐户（例如 `sa-mssql-controller` 或 `master`）来协调群集 Pod、服务、高可用性、监视等的预配。当 BDC 部署启动（例如 `azdata bdc create`）时，`azdata` 执行以下操作：

1. 检查提供的命名空间是否存在。
2. 如果不存在，将创建一个，并应用 `MSSQL_CLUSTER` 标签。
3. 创建 `sa-mssql-controller` 服务帐户。
4. 创建对命名空间或项目具有完全权限但不是群集级别权限的 `<namespaced>-admin` 角色。
5. 为角色创建该服务帐户的角色分配。

完成这些步骤后，预配控制平面 Pod，并且服务帐户将部署大数据群集的其余部分。  

因此，进行部署的用户必须具有执行以下操作的权限：

- 列出群集中的命名空间 (1)。
- 用标签修补新的或现有的命名空间 (2)。
- 创建服务帐户 `sa-mssql-controller`、`<namespaced>-admin` 角色和角色绑定 (3-5)。

默认 `admin` 角色不具有这些权限，因此部署大数据群集的用户必须至少具有命名空间级别的管理员权限。

## <a name="cluster-role-required-for-pods-and-nodes-metrics-collection"></a>收集 Pod 和节点指标所需的群集角色

从 SQL Server 2019 CU5 开始，Telegraf 需要具有群集级别角色权限的服务帐户来收集 Pod 和节点指标。 部署（或者升级现有部署）期间，尝试创建必要的服务帐户和群集角色，但如果部署群集或执行升级的用户没有足够的权限，部署或升级将在出现警告的情况下继续进行并获得成功。 这种情况下，不会收集 Pod 和节点指标。 部署群集的用户必须要求群集管理员创建角色和服务帐户（部署或升级之前或之后）。 创建后，BDC 将使用它们。 

下面的脚本演示如何创建所需项目：

```console
export CLUSTER_NAME=mssql-cluster
kubectl create -f - <<EOF
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: ${CLUSTER_NAME}:cr-mssql-metricsdc-reader
rules:
- apiGroups:
  - '*'
  resources:
  - pods
  - nodes/stats
  verbs:
  - get
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: ${CLUSTER_NAME}:crb-mssql-metricsdc-reader
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: ${CLUSTER_NAME}:cr-mssql-metricsdc-reader
subjects:
- kind: ServiceAccount
  name: sa-mssql-metricsdc-reader
  namespace: ${CLUSTER_NAME}
EOF
```

服务帐户、群集角色和群集角色绑定可以在 BDC 部署之前或之后创建。 Kubernetes 自动更新 Telegraf 服务帐户的权限。 如果这些帐户和角色创建为 Pod 部署，将在收集的 Pod 和节点指标中看到几分钟的延迟。

> [!NOTE]
> SQL Server 2019 CU5 引入了两个功能开关来控制 Pod 和节点指标的收集。 默认情况下，这些参数在所有环境目标中都设为 true，除了重写默认值的 OpenShift。 

可以在 `control.json` 部署配置文件的安全性部分中自定义这些设置：

```json
  "security": {
    …
    "allowNodeMetricsCollection": false,
    "allowPodMetricsCollection": false
  }
```

如果这些设置设为 `false`，则 BDC 部署工作流不会尝试为 Telegraf 创建服务帐户、群集角色和绑定。
