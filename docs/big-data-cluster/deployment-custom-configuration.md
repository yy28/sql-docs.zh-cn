---
title: 配置部署
titleSuffix: SQL Server big data clusters
description: 了解如何使用配置文件自定义大数据群集部署。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
manager: jroth
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 19654422bcc57f2ad00b9ab8170d163f848f188b
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2019
ms.locfileid: "67728890"
---
# <a name="configure-deployment-settings-for-big-data-clusters"></a>配置大数据群集的部署设置

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

若要自定义群集部署配置文件，可以使用任何 JSON 格式编辑器，如 VSCode。 脚本编写用于自动化目的这些编辑，请使用**mssqlctl bdc 配置节**命令。 本文介绍如何通过修改部署配置文件配置的大数据群集部署。 它提供了有关如何更改为不同的方案配置的示例。 有关如何在部署中使用的配置文件的详细信息，请参阅[部署指南](deployment-guidance.md#configfile)。

## <a name="prerequisites"></a>先决条件

- [安装 mssqlctl](deploy-install-mssqlctl.md)。

- 每个此部分中的示例假设您已创建一份标准配置文件之一。 有关详细信息，请参阅[创建自定义配置文件](deployment-guidance.md#customconfig)。 例如，以下命令将创建一个名为目录`custom`，其中包含基于默认值的 JSON 部署配置文件**aks 开发测试**配置：

   ```bash
   mssqlctl bdc config init --source aks-dev-test --target custom
   ```

## <a id="clustername"></a> 更改群集名称

群集名称是名称大数据群集，将创建部署的 Kubernetes 命名空间。 它是在部署配置文件的以下部分中指定的：

```json
"metadata": {
    "kind": "Cluster",
    "name": "mssql-cluster"
},
```

以下命令将发送到的键-值对 **--json 值**参数，以更改到的大数据群集名称**测试群集**:

```bash
mssqlctl bdc config section set --config-profile custom -j "metadata.name=test-cluster"
```

> [!IMPORTANT]
> 大数据群集的名称必须仅小写字母数字字符，不留空格。 将在具有与群集相同的名称的命名空间中创建群集的所有 Kubernetes 项目 （容器、 pod、 有状态集、 服务） 指定的名称。

## <a id="ports"></a> 更新终结点端口

为控制平面以及单个池与定义终结点。 配置文件的以下部分显示了控制平面的终结点定义：

```json
"endpoints": [
    {
        "name": "Controller",
        "serviceType": "LoadBalancer",
        "port": 30080
    },
    {
        "name": "ServiceProxy",
        "serviceType": "LoadBalancer",
        "port": 30777
    }
]
```

下面的示例使用内联 JSON 若要更改的端口**控制器**终结点：

```bash
mssqlctl bdc config section set --config-profile custom -j "$.spec.controlPlane.spec.endpoints[?(@.name==""Controller"")].port=30000"
```

## <a id="replicas"></a> 配置池副本

在配置文件中定义的每个池，如存储池的特征。 例如，以下部分显示了存储池定义：

```json
"pools": [
    {
        "metadata": {
            "kind": "Pool",
            "name": "default"
        },
        "spec": {
            "type": "Storage",
            "replicas": 2,
            "storage": {
               "data": {
                  "className": "default",
                  "accessMode": "ReadWriteOnce",
                  "size": "15Gi"
               },
               "logs": {
                  "className": "default",
                  "accessMode": "ReadWriteOnce",
                  "size": "10Gi"
               }
           },
        }
    }
]
```

可以通过修改在池中配置的实例数**副本**每个池的值。 下面的示例使用内联 JSON 可以更改这些值到的存储和数据池`10`和`4`分别：

```bash
mssqlctl bdc config section set --config-profile custom -j "$.spec.pools[?(@.spec.type == ""Storage"")].spec.replicas=10"
mssqlctl bdc config section set --config-profile custom -j "$.spec.pools[?(@.spec.type == ""Data"")].spec.replicas=4"
```

## <a id="storage"></a> 配置存储

此外可以更改的存储类和用于每个池的特征。 下面的示例向存储池分配自定义的存储类，并更新存储 100 gb 数据的永久性卷声明的大小。 本部分中必须要使用更新设置的配置文件*mssqlctl bdc 配置集*命令，请参阅如何使用修补程序文件来将此部分添加下面：

```bash
mssqlctl bdc config section set --config-profile custom -j "$.spec.pools[?(@.spec.type == ""Storage"")].spec.storage.data.className=storage-pool-class"
mssqlctl bdc config section set --config-profile custom -j "$.spec.pools[?(@.spec.type == ""Storage"")].spec.storage.data.size=32Gi"
```

> [!NOTE]
> 配置文件基于**kubeadm 开发测试**不具有存储定义的每个池，但这可以手动添加必要。

有关存储配置的详细信息，请参阅[与大数据群集在 Kubernetes 的 SQL Server 数据暂留](concept-data-persistence.md)。

## <a id="sparkstorage"></a> 配置存储，没有 spark

此外可以配置存储池没有 spark 的情况下运行并创建一个单独的 spark 池。 这使您能够缩放 spark 计算 power 独立于存储。 若要了解如何配置 spark 池，请参阅[JSON 修补程序文件示例](#jsonpatch)本文结尾处。

本部分中必须要使用更新设置的配置文件`mssqlctl cluster config set command`。 以下 JSON 修补程序文件演示如何将此添加。

默认情况下**includeSpark**设置为存储池设置为 true，因此必须添加**includeSpark**字段以便更改的存储配置：

```bash
mssqlctl cluster config section set --config-profile custom -j "$.spec.pools[?(@.spec.type == ""Storage"")].includeSpark=false"
```

## <a id="podplacement"></a> 配置使用 Kubernetes 标签的 pod 位置

您可以控制在有特定的资源以适应各种类型的工作负荷要求的 Kubernetes 节点上 pod 放置。 例如，你可能想要确保使用多个存储节点上放置存储池 pod 或 SQL Server 主实例均放置在具有更快的 CPU 和内存资源的节点上。 在这种情况下，您将首先生成具有不同类型的硬件的异类 Kubernetes 群集，然后[将节点标签分配](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)相应地。 部署大数据群集时，可以在群集部署配置文件中指定相同的标签，在池级别。 Kubernetes 然后会处理的关联与指定的标签匹配的节点上 pod。

下面的示例显示了如何编辑要包含的 SQL Server 主实例的节点标签设置的自定义配置文件。 请注意，没有任何*nodeLabel*密钥在内置的配置中，因此将需要手动编辑自定义配置文件或创建修补程序文件并将其应用于自定义配置文件。

创建名为的文件**patch.json**包含以下内容在当前目录中：

```json
{
  "patch": [
     {
      "op": "add",
      "path": "$.spec.pools[?(@.spec.type == 'Master')].spec",
      "value": {
      "nodeLabel": "<yourNodeLabel>"
       }
    }
  ]
}
```

```bash
mssqlctl bdc config section set --config-profile custom -p ./patch.json
```

## <a id="jsonpatch"></a> JSON 修补程序文件

JSON 修补程序文件一次配置多个设置。 有关 JSON 修补程序的详细信息，请参阅[在 Python 中的 JSON 修补程序](https://github.com/stefankoegl/python-json-patch)并[JSONPath 联机计算器](https://jsonpath.com/)。

以下**patch.json**文件执行以下更改：

- 更新单个终结点的端口。
- 更新所有终结点 (**端口**并**serviceType**)。
- 更新控制平面存储。 这些设置是适用于所有群集组件，除非在池级别重写。
- 更新控制平面存储中的存储类名称。
- 更新存储池的池存储设置。
- 更新存储池的 Spark 设置。
- 使用 2 个副本用于群集创建 spark 池

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "$.spec.controlPlane.spec.endpoints[?(@.name=='Controller')].port",
      "value": 30000
    },
    {
      "op": "replace",
      "path": "spec.controlPlane.spec.endpoints",
      "value": [
        {
          "serviceType": "LoadBalancer",
          "port": 30001,
          "name": "Controller"
        },
        {
            "serviceType": "LoadBalancer",
            "port": 30778,
            "name": "ServiceProxy"
        }
      ]
    },
    {
      "op": "replace",
      "path": "spec.controlPlane.spec.controlPlane",
      "value": {
          "data": {
            "className": "managed-premium",
            "accessMode": "ReadWriteOnce",
            "size": "100Gi"
          },
          "logs": {
            "className": "managed-premium",
            "accessMode": "ReadWriteOnce",
            "size": "32Gi"
          }
        }
    },
    {
      "op": "replace",
      "path": "spec.controlPlane.spec.storage.data.className",
      "value": "managed-premium"
    },
    {
      "op": "add",
      "path": "$.spec.pools[?(@.spec.type == 'Storage')].spec.storage",
      "value": {
          "data": {
            "className": "managed-premium",
            "accessMode": "ReadWriteOnce",
            "size": "100Gi"
          },
          "logs": {
            "className": "managed-premium",
            "accessMode": "ReadWriteOnce",
            "size": "32Gi"
          }
        }
    },
    {
      "op": "replace",
      "path": "$.spec.pools[?(@.spec.type == 'Storage')].hadoop.spark",
      "value": {
        "driverMemory": "2g",
        "driverCores": 1,
        "executorInstances": 3,
        "executorCores": 1,
        "executorMemory": "1536m"
      }
    },
    {
      "op": "add",
      "path": "spec.pools/-",
      "value":
      {
        "metadata": {
          "kind": "Pool",
          "name": "default"
        },
        "spec": {
          "type": "Spark",
          "replicas": 2
        },
        "hadoop": {
          "yarn": {
            "nodeManager": {
              "memory": 12288,
              "vcores": 6
            },
            "schedulerMax": {
              "memory": 12288,
              "vcores": 6
            },
            "capacityScheduler": {
              "maxAmPercent": 0.3
            }
          },
          "spark": {
            "driverMemory": "2g",
            "driverCores": 1,
            "executorInstances": 2,
            "executorMemory": "2g",
            "executorCores": 1
          }
        }
      }
    }   
  ]
}
```

> [!TIP]
> 结构和选项的更改部署配置文件的详细信息，请参阅[适用于大数据群集的部署配置文件引用](reference-deployment-config.md)。

使用**mssqlctl bdc 配置部分，设置**应用 JSON 修补程序文件中的更改。 下面的示例应用**patch.json**到目标部署配置文件的文件**custom.json**。

```bash
mssqlctl bdc config section set --config-profile custom -p ./patch.json
```

## <a name="next-steps"></a>后续步骤

有关使用大数据群集部署中的配置文件的详细信息，请参阅[如何部署 SQL Server 大数据群集在 Kubernetes 上](deployment-guidance.md#configfile)。
