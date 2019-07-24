---
title: 配置部署
titleSuffix: SQL Server big data clusters
description: 了解如何使用配置文件自定义大数据群集部署。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d7559ecf9c7b17ca21c088ed531a347f88e89ee2
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419434"
---
# <a name="configure-deployment-settings-for-big-data-clusters"></a>为大数据群集配置部署设置

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

若要自定义群集部署配置文件, 可以使用任何 JSON 格式编辑器, 如 VSCode。 出于自动化目的编写这些编辑的脚本时, 请使用**azdata bdc config**命令。 本文介绍如何通过修改部署配置文件来配置大数据群集部署。 其中提供了有关如何更改不同方案的配置的示例。 有关如何在部署中使用配置文件的详细信息, 请参阅[部署指南](deployment-guidance.md#configfile)。

## <a name="prerequisites"></a>先决条件

- [安装 azdata](deploy-install-azdata.md)。

- 本部分中的每个示例假设已创建一个标准配置的副本。 有关详细信息, 请参阅[创建自定义配置](deployment-guidance.md#customconfig)。 例如, 下面的命令创建一个名`custom`为的目录, 其中包含两个基于默认 **aks**配置的 json 部署配置文件:

   ```bash
   azdata bdc config init --source aks-dev-test --target custom
   ```

## <a id="clustername"></a>更改群集名称

群集名称既是大数据群集的名称, 也是在部署时创建的 Kubernetes 命名空间的名称。 它在**cluster**部署配置文件的以下部分中指定:

```json
"metadata": {
    "kind": "Cluster",
    "name": "mssql-cluster"
},
```

以下命令将键值对发送到 **--json 值**参数, 以将大数据群集名称更改为**测试群集**:

```bash
azdata bdc config replace --config-file custom/cluster.json --json-values "metadata.name=test-cluster"
```

> [!IMPORTANT]
> 大数据群集的名称必须仅包含小写字母数字字符, 不能包含空格。 将在命名空间中创建群集的所有 Kubernetes 项目 (容器、pod、有状态 "集、服务), 该命名空间与指定的群集名称具有相同的名称。

## <a id="ports"></a>更新终结点端口

终结点是在**cluster**中的相应部分为 "json" 和 "网关" 和 "SQL Server 主实例" 中的控制器定义的 **。** 下面的**控件 json**配置文件部分显示控制器的终结点定义:

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

下面的示例使用内联 JSON 更改**控制器**终结点的端口:

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.endpoints[?(@.name==""Controller"")].port=30000"
```

## <a id="replicas"></a>配置池副本

每个池的特征 (例如存储池) 都是在**cluster**配置文件中定义的。 例如, **cluster**的以下部分显示了存储池定义:

```json
"pools": [
   {
       "metadata": {
           "kind": "Pool",
           "name": "default"
       },
       "spec": {
           "type": "Storage",
           "replicas": 2
       }
   }
]
```

可以通过修改每个池的**副本**值来配置池中的实例数。 下面的示例使用内联 JSON `10` `4`分别更改存储和数据池的这些值:

```bash
azdata bdc config replace --config-file custom/cluster.json --json-values "$.spec.pools[?(@.spec.type == ""Storage"")].spec.replicas=10"
azdata bdc config replace --config-file custom/cluster.json --json-values "$.spec.pools[?(@.spec.type == ""Data"")].spec.replicas=4"
```

## <a id="storage"></a>配置存储

你还可以更改用于每个池的存储类和特性。 下面的示例将自定义存储类分配给存储池, 并更新永久性卷声明的大小, 以便将数据存储到100Gb。 首先创建一个包含新*存储*部分 (除了*类型*和*副本*) 的 patch. json 文件

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "$.spec.pools[?(@.spec.type == 'Storage')].spec",
      "value": {
        "storage":{
        "data":{
                "size": "100Gi",
                "className": "myStorageClass",
                "accessMode":"ReadWriteOnce"
                },
        "logs":{
                "size":"32Gi",
                "className":"myStorageClass",
                "accessMode":"ReadWriteOnce"
                }
                },
        "type":"Storage",
        "replicas":2
      }
    }
  ]
}
```

然后, 可以使用**azdata bdc 配置修补程序**命令更新**cluster**配置文件。
```bash
azdata bdc config patch --config-file custom/cluster.json --patch ./patch.json
```

> [!NOTE]
> 基于**kubeadm**的配置文件不具有每个池的存储定义, 但你可以根据需要使用上面的进程进行添加。

有关存储配置的详细信息, 请参阅[Kubernetes 上的数据暂留 SQL Server 大数据群集](concept-data-persistence.md)。

## <a id="sparkstorage"></a>不带 spark 配置存储池

你还可以将存储池配置为在不使用 spark 的情况下运行, 并创建单独的 spark 池。 这使你可以扩展独立于存储的 spark 计算能力。 若要查看如何配置 spark 池, 请参阅本文末尾的[JSON patch 文件示例](#jsonpatch)。



默认情况下, 存储池的**includeSpark**设置设置为 true, 因此必须将**includeSpark**字段添加到存储配置中才能进行更改。 下面的 JSON 修补程序文件显示了如何添加此项。

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "$.spec.pools[?(@.spec.type == 'Storage')].spec",
      "value": {
        "type":"Storage",
        "replicas":2,
        "includeSpark":false
      }
    }
  ]
}
```

```bash
azdata bdc config patch --config-file custom/cluster.json --patch ./patch.json
```

## <a id="podplacement"></a>使用 Kubernetes 标签配置 pod 布局

可以控制 Kubernetes 节点上的 pod 位置, 这些节点具有特定的资源, 可适应各种类型的工作负荷要求。 例如, 你可能想要确保将存储池 pod 放置在具有更多存储的节点上, 或者将 SQL Server 主实例放置在 CPU 和内存资源较高的节点上。 在这种情况下, 你将首先构建包含不同类型硬件的异类 Kubernetes 群集, 然后相应地[分配节点标签](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)。 部署大数据群集时, 可以在群集部署配置文件中的池级别指定相同标签。 然后, Kubernetes 将负责层面与指定标签匹配的节点上的箱。

下面的示例演示如何编辑自定义配置文件以包括 SQL Server 主实例的节点标签设置。 请注意, 在内置配置中没有*nodeLabel*密钥, 因此你将需要手动编辑自定义配置文件, 或者创建一个修补程序文件并将其应用于自定义配置文件。

在当前目录中创建一个名为 " **patch** " 的文件, 其中包含以下内容:

```json
{
  "patch": [
     {
      "op": "replace",
      "path": "$.spec.pools[?(@.spec.type == 'Master')].spec",
      "value": {
           "type": "Master",
         "replicas": 1,
         "hadrEnabled": false,
         "endpoints": [
            {
             "name": "Master",
             "serviceType": "NodePort",
             "port": 31433
            }
          ],
         "nodeLabel": "<yourNodeLabel>"
       }
    }
  ]
}
```

```bash
azdata bdc config patch --config-file custom/cluster.json --patch-file ./patch.json
```

## <a id="jsonpatch"></a>JSON 修补程序文件

JSON 修补程序文件同时配置多个设置。 有关 JSON 修补程序的详细信息, 请参阅[Python 中的 Json 修补程序](https://github.com/stefankoegl/python-json-patch)和[JSONPath Online 计算器](https://jsonpath.com/)。

以下**patch json**文件执行以下更改:

- 更新**控件 json**中单个终结点的端口。
    ```json
    {
      "patch": [
        {
          "op": "replace",
          "path": "$.spec.endpoints[?(@.name=='Controller')].port",
          "value": 30000
        }   
      ]
    }
    ```

- 更新**控件 json**中的所有终结点 (**端口**和**serviceType**)。
    ```json
    {
      "patch": [
        {
          "op": "replace",
          "path": "spec.endpoints",
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
        }
      ]
    }
    ```

- 更新**控件 json**中的控制器存储设置。 除非在池级别重写, 否则这些设置适用于所有群集组件。
    ```json
    {
      "patch": [
        {
          "op": "replace",
          "path": "spec.storage",
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
        }   
      ]
    }
    ```

- 更新**控件 json**中的存储类名称。
    ```json
    {
      "patch": [
        {
          "op": "replace",
          "path": "spec.storage.data.className",
          "value": "managed-premium"
        }   
      ]
    }
    ```

- 更新**群集**中存储池的池存储设置。
    ```json
    {
      "patch": [
        {
          "op": "replace",
          "path": "$.spec.pools[?(@.spec.type == 'Storage')].spec",
          "value": {
        "type":"Storage",
        "replicas":2,
        "storage":{
        "data":{
            "size": "100Gi",
            "className": "myStorageClass",
            "accessMode":"ReadWriteOnce"
            },
        "logs":{
            "size":"32Gi",
            "className":"myStorageClass",
            "accessMode":"ReadWriteOnce"
            }
            }
         }
        }
      ]
    }
    ```

- 更新**群集**中存储池的 Spark 设置。
    ```json
    {
      "patch": [
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
        }   
      ]
    }
    ```

- 使用**cluster**中的2个实例创建一个 spark 池。
    ```json
    {
      "patch": [
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
> 有关用于更改部署配置文件的结构和选项的详细信息, 请参阅[适用于大数据群集的部署配置文件引用](reference-deployment-config.md)。

使用**azdata bdc config**命令应用 JSON 修补文件中的更改。 下面的示例将**patch**文件应用到目标部署配置文件**自定义/cluster。**

```bash
azdata bdc config patch --config-file custom/cluster.json --patch-file ./patch.json
```

## <a name="next-steps"></a>后续步骤

有关在大数据群集部署中使用配置文件的详细信息, 请参阅[如何在 Kubernetes 上部署 SQL Server 大数据群集](deployment-guidance.md#configfile)。
