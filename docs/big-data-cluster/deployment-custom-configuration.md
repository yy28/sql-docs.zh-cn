---
title: 配置部署
titleSuffix: SQL Server big data clusters
description: 了解如何使用配置文件自定义大数据群集部署。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 02e922ca909cd863d496f9c49a60dd986df8bedb
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2019
ms.locfileid: "69652395"
---
# <a name="configure-deployment-settings-for-big-data-clusters"></a>配置大数据群集的部署设置

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

要自定义集群部署配置文件，可以使用任何 JSON 格式编辑器，例如 VSCode。 如果需要出于自动化目的为这些编辑内容编写脚本，请使用“azdata bdc config”命令。 本文介绍如何通过修改部署配置文件来配置大数据群集部署。 它提供了为不同方案更改配置的示例。 有关如何在部署中使用配置文件的详细信息，请参阅[部署指南](deployment-guidance.md#configfile)。

## <a name="prerequisites"></a>先决条件

- [安装 azdata](deploy-install-azdata.md)。

- 本部分中的每个示例都假定已创建一个标准配置的副本。 有关详细信息，请参阅[创建自定义配置](deployment-guidance.md#customconfig)。 例如，以下命令根据默认的“aks-dev-test”配置创建一个名为 `custom` 的目录，其中包含两个 JSON 部署配置文件“cluster.json”和“control.json”：

   ```bash
   azdata bdc config init --source aks-dev-test --target custom
   ```

## <a id="clustername"></a> 更改群集名称

群集名称既是大数据群集的名称，也是将在部署时创建的 Kubernetes 命名空间的名称。 它在“cluster.json”部署配置文件的以下部分中指定：

```json
"metadata": {
    "kind": "Cluster",
    "name": "mssql-cluster"
},
```

以下命令将键值对发送到“--json-values”参数，将大数据集群名称更改为“test-cluster”：

```bash
azdata bdc config replace --config-file custom/cluster.json --json-values "metadata.name=test-cluster"
```

> [!IMPORTANT]
> 大数据群集的名称只能使用小写的字母数字字符，不能有空格。 将在与指定的群集名称同名的命名空间中创建群集的所有 Kubernetes 项目（容器、pod、状态集、服务）。

## <a id="ports"></a> 更新终结点端口

在“control.json”中为控制器定义终结点，在“cluster.json”的相应部分中为网关和 SQL Server 主实例定义终结点。 “control.json”配置文件的以下部分显示了控制器的终结点定义：

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

以下示例使用内联 JSON 更改“控制器”终结点的端口：

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.endpoints[?(@.name==""Controller"")].port=30000"
```

## <a id="replicas"></a> 配置池副本

每个池的特征（例如存储池）都在“cluster.json”配置文件中定义。 例如，“cluster.json”的以下部分显示了存储池定义：

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

可以通过修改每个池的“副本”值来配置池中的实例数。 以下示例使用内联 JSON 将存储和数据池的这些值分别更改为 `10` 和 `4`：

```bash
azdata bdc config replace --config-file custom/cluster.json --json-values "$.spec.pools[?(@.spec.type == ""Storage"")].spec.replicas=10"
azdata bdc config replace --config-file custom/cluster.json --json-values "$.spec.pools[?(@.spec.type == ""Data"")].spec.replicas=4"
```

## <a id="storage"></a> 配置存储

还可以更改用于每个池的存储类和特征。 以下示例将自定义存储类分配给存储池，并更新用于将数据存储到 100Gb 的永久性卷声明的大小。 首先创建一个 patch.json 文件，如下所示，除了类型和副本之外，还包括新的存储部分

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

然后，可以使用“azdata bdc config patch”命令更新“cluster.json”配置文件。
```bash
azdata bdc config patch --config-file custom/cluster.json --patch ./patch.json
```

> [!NOTE]
> 基于 kubeadm-dev-test 的配置文件不含每个池的存储定义，但可以根据需要使用上面的过程来添加。

有关存储配置的详细信息，请参阅 [Kubernetes 上 SQL Server 大数据群集的数据暂留](concept-data-persistence.md)。

## <a id="sparkstorage"></a> 配置不使用 spark 的存储池

还可以将存储池配置为在没有 spark 的情况下运行，并创建单独的 spark 池。 这样可以独立于存储来扩展 spark 计算能力。 若要了解如何配置 spark 池，请参阅本文末尾的 [JSON 修补程序文件示例](#jsonpatch)。



默认情况下，存储池的“includeSpark”设置设为 true，因此需要将 includeSpark 字段添加到存储配置中才能进行更改。 以下 JSON 修补程序文件显示了如何添加该字段。

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

## <a id="podplacement"></a> 使用 Kubernetes 标签配置 pod 布局

可以控制具有特定资源的 Kubernetes 节点上的 pod 放置，以适应各种类型的工作负载要求。 例如，你可能会想确保将存储池 pod 放置在具有更多存储的节点上，或者将 SQL Server 主实例放置在具有更高 CPU 和更多内存资源的节点上。 在这种情况下，需首先构建具有不同类型硬件的异类 Kubernetes 群集，然后相应[分配节点标签](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)。 部署大数据群集时，可在群集部署配置文件中，在池级别指定相同的标签。 然后，kubernetes 负责将与指定标签匹配的节点上的 pod 关联起来。 需要添加到 kubernetes 群集中节点的特定标签键是**mssql 群集范围内**的。 此标签本身的值可以是所选择的任何字符串。

下面的示例演示如何编辑自定义配置文件以包括 SQL Server 主实例、计算池、数据池 & 存储池的节点标签设置。 请注意，内置配置中没有 nodeLabel 键，因此需要手动编辑自定义配置文件或创建修补程序文件并将其应用于自定义配置文件。 SQL Server 的主实例 pod 将部署在一个节点上, 该节点包含具有值**bdc-Master**的标签**mssql-群集**。 计算池和数据池箱将部署在包含一个标签为**mssql-群集**的节点上, 其值为 " **bdc-sql**"。 存储池将部署在一个节点上, 在该节点上, 其值为 "bdc-**群集**-**存储**"。

在当前目录中创建名为“patch.json”的文件，其内容如下：

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
        "nodeLabel": "bdc-master"
      }
    },
    {
      "op": "replace",
      "path": "$.spec.pools[?(@.spec.type == 'Compute')].spec",
      "value": {
    "type": "Compute",
        "replicas": 1,
        "nodeLabel": "bdc-sql"
      }
    },
    {
      "op": "replace",
      "path": "$.spec.pools[?(@.spec.type == 'Data')].spec",
      "value": {
    "type": "Data",
        "replicas": 2,
        "nodeLabel": "bdc-sql"
      }
    },
    {
      "op": "replace",
      "path": "$.spec.pools[?(@.spec.type == 'Storage')].spec",
      "value": {
    "type": "Storage",
        "replicas": 3,
        "nodeLabel": "bdc-storage"
      }
    }
  ]
}
```

```bash
azdata bdc config patch --config-file custom/cluster.json --patch-file ./patch.json
```

## <a id="jsonpatch"></a> JSON 修补程序文件

JSON 修补程序文件一次配置多个设置。 有关 JSON 修补程序的详细信息，请参阅 [python 中的 JSON 修补程序](https://github.com/stefankoegl/python-json-patch)和 [JSONPath 联机计算器](https://jsonpath.com/)。

以下“patch.json”文件执行以下更改：

- 更新“control.json”中单个终结点的端口。
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

- 更新“control.json”中的所有终结点（“端口”和“servicetype”）。
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

- 更新“control.json”中的控制器存储设置。 除非在池级别重写，否则这些设置适用于所有群集组件。
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

- 更新“control.json”中的存储类名称。
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

- 更新”cluster.json”中存储池的池存储设置。
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

- 更新”cluster.json”中存储池的 Spark 设置。
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

- 在“cluster.json”中创建一个包含 2 个实例的 spark 池。
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
> 有关部署配置文件的结构和用于更改该文件的选项的更多信息，请参阅[大数据群集的部署配置文件参考](reference-deployment-config.md)。

使用“azdata bdc config”命令来应用 json 修补程序文件中的更改。 下面的示例将“patch.json”文件应用于目标部署配置文件“custom/cluster.json”。

```bash
azdata bdc config patch --config-file custom/cluster.json --patch-file ./patch.json
```

## <a name="next-steps"></a>后续步骤

有关在大数据群集部署中使用配置文件的详细信息, 请参阅[如何[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]在 Kubernetes 上部署](deployment-guidance.md#configfile)。
