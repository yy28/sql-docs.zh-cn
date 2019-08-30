---
title: 配置部署
titleSuffix: SQL Server big data clusters
description: 了解如何使用配置文件自定义大数据群集部署。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 230ec2300bff55cefbb176c69d677b4e04d6ad30
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155323"
---
# <a name="configure-deployment-settings-for-cluster-resources-and-services"></a>为群集资源和服务配置部署设置

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

从 azdata 管理工具中内置的预定义配置文件集开始, 你可以轻松地修改默认设置, 以便更好地满足你的 BDC 工作负荷要求。 从候选发布版本开始, 已更新配置文件的结构, 使你能够按资源的每个服务以粒度方式更新设置。 

还可以设置资源级别配置或更新资源中所有服务的配置。 下面是用于**bdc**的结构的摘要:

```json
{
    "apiVersion": "v1",
    "metadata": {
        "kind": "BigDataCluster",
        "name": "mssql-cluster"
    },
    "spec": {
        "resources": {
            "nmnode-0": {...
            },
            "sparkhead": {...
            },
            "zookeeper": {...
            },
            "gateway": {...
            },
            "appproxy": {...
            },
            "master": {...
            },
            "compute-0": {...
            },
            "data-0": {...
            },
            "storage-0": {...
        },
        "services": {
            "sql": {
                "resources": [
                    "master",
                    "compute-0",
                    "data-0",
                    "storage-0"
                ]
            },
            "hdfs": {
                "resources": [
                    "nmnode-0",
                    "zookeeper",
                    "storage-0",
                    "sparkhead"
                ],
                "settings": {...
            },
            "spark": {
                "resources": [
                    "sparkhead",
                    "storage-0"
                ],
                "settings": {...
            }
        }
    }
}
```

若要更新资源级别配置 (如池中的实例), 需要更新资源规格。例如, 若要更新计算池中的实例数, 请在**bdc. json**配置文件中修改此部分:
```json
"resources": {
    ...
    "compute-0": {
        "metadata": {
            "kind": "Pool",
            "name": "default"
        },
        "spec": {
            "type": "Compute",
            "replicas": 4
        }
    }
    ...
}
``` 

类似于在特定资源中更改单一服务的设置。 例如, 如果只想更改存储池中 Spark 组件的 Spark 内存设置, 则将使用 udpate 配置文件中**spark**服务的 "设置" 部分来**设置** **存储 0**资源.
```json
"resources":{
    ...
     "storage-0": {
        "metadata": {
            "kind": "Pool",
            "name": "default"
        },
        "spec": {
            "type": "Storage",
            "replicas": 2,
            "settings": {
                "spark": {
                    "driverMemory": "2g",
                    "driverCores": "1",
                    "executorInstances": "3",
                    "executorMemory": "1536m",
                    "executorCores": "1"
                }
            }
        }
    }
    ...
}
```

如果要对与多个资源关联的服务应用相同的配置, 则需要在 "**服务**" 部分中更新相应的**设置**。 例如, 如果你想要跨存储池和 Spark 池为 Spark 设置相同的设置, 则将更新 "" 的 "**设置**" 部分。

```json
"services": {
    ...
    "spark": {
        "resources": [
            "sparkhead",
            "storage-0"
        ],
        "settings": {
            "driverMemory": "2g",
            "driverCores": "1",
            "executorInstances": "3",
            "executorMemory": "1536m",
            "executorCores": "1"
        }
    }
    ...
}
```


要自定义集群部署配置文件，可以使用任何 JSON 格式编辑器，例如 VSCode。 如果需要出于自动化目的为这些编辑内容编写脚本，请使用“azdata bdc config”命令。 本文介绍如何通过修改部署配置文件来配置大数据群集部署。 它提供了为不同方案更改配置的示例。 有关如何在部署中使用配置文件的详细信息，请参阅[部署指南](deployment-guidance.md#configfile)。

## <a name="prerequisites"></a>先决条件

- [安装 azdata](deploy-install-azdata.md)。

- 本部分中的每个示例都假定已创建一个标准配置的副本。 有关详细信息，请参阅[创建自定义配置](deployment-guidance.md#customconfig)。 例如, 下面的命令创建一个名`custom`为的目录, 其中包含两个基于默认 **aks**配置的 json部署配置文件:

   ```bash
   azdata bdc config init --source aks-dev-test --target custom
   ```

## <a id="clustername"></a> 更改群集名称

群集名称既是大数据群集的名称，也是将在部署时创建的 Kubernetes 命名空间的名称。 它在**bdc json**部署配置文件的以下部分中指定:

```json
"metadata": {
    "kind": "BigDataCluster",
    "name": "mssql-cluster"
},
```

以下命令将键值对发送到“--json-values”参数，将大数据集群名称更改为“test-cluster”：

```bash
azdata bdc config replace --config-file custom/bdc.json --json-values "metadata.name=test-cluster"
```

> [!IMPORTANT]
> 大数据群集的名称只能使用小写的字母数字字符，不能有空格。 将在与指定的群集名称同名的命名空间中创建群集的所有 Kubernetes 项目（容器、pod、状态集、服务）。

## <a id="ports"></a> 更新终结点端口

终结点是为**控件 json**中的控制器定义的, 并为网关和 SQL Server master 实例定义。 “control.json”配置文件的以下部分显示了控制器的终结点定义：

```json
{
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
}
```

以下示例使用内联 JSON 更改“控制器”终结点的端口：

```bash
azdata bdc config replace --config-file custom/control.json --json-values "$.spec.endpoints[?(@.name==""Controller"")].port=30000"
```

## <a id="replicas"></a> 配置池副本

每个资源的配置 (如存储池) 都是在**bdc json**配置文件中定义的。 例如, 以下部分的**bdc**显示**存储空间的**资源定义:

```json
"storage-0": {
    "metadata": {
        "kind": "Pool",
        "name": "default"
    },
    "spec": {
        "type": "Storage",
        "replicas": 2,
        "settings": {
            "spark": {
                "driverMemory": "2g",
                "driverCores": "1",
                "executorInstances": "3",
                "executorMemory": "1536m",
                "executorCores": "1"
            }
        }
    }
}
```

可以通过修改每个池的“副本”值来配置池中的实例数。 以下示例使用内联 JSON 将存储和数据池的这些值分别更改为 `10` 和 `4`：

```bash
azdata bdc config replace --config-file custom/bdc.json --json-values "$.spec.resources.storage-0.spec.replicas=10"
azdata bdc config replace --config-file custom/bdc.json --json-values "$.spec.resources.data-0.spec.replicas=4"
```

## <a id="storage"></a> 配置存储

还可以更改用于每个池的存储类和特征。 以下示例将自定义存储类分配给存储池，并更新用于将数据存储到 100Gb 的永久性卷声明的大小。 首先创建一个 patch.json 文件，如下所示，除了类型和副本之外，还包括新的存储部分

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "spec.resources.storage-0.spec",
      "value": {
        "type": "Storage",
        "replicas": 2,
        "storage": {
          "data": {
            "size": "100Gi",
            "className": "myStorageClass",
            "accessMode": "ReadWriteOnce"
          },
          "logs": {
            "size": "32Gi",
            "className": "myStorageClass",
            "accessMode": "ReadWriteOnce"
          }
        }
      }
    }
  ]
}
```

然后, 你可以使用**azdata bdc 配置修补程序**命令更新**bdc json**配置文件。
```bash
azdata bdc config patch --config-file custom/bdc.json --patch ./patch.json
```

> [!NOTE]
> 基于 kubeadm-dev-test 的配置文件不含每个池的存储定义，但可以根据需要使用上面的过程来添加。

有关存储配置的详细信息，请参阅 [Kubernetes 上 SQL Server 大数据群集的数据暂留](concept-data-persistence.md)。

## <a id="sparkstorage"></a> 配置不使用 spark 的存储池

还可以将存储池配置为在没有 spark 的情况下运行，并创建单独的 spark 池。 这样可以独立于存储来扩展 spark 计算能力。 若要了解如何配置 spark 池，请参阅本文末尾的 [JSON 修补程序文件示例](#jsonpatch)。


默认情况下, 存储池资源的**includeSpark**设置设置为 true, 因此必须将**includeSpark**字段编辑为存储配置, 才能进行更改。 以下命令演示如何使用内联 json 编辑此值。

```bash
azdata bdc config replace --config-file custom/bdc.json --json-values "$.spec.resources.storage-0.spec.settings.spark.includeSpark=false"
```

## <a id="podplacement"></a> 使用 Kubernetes 标签配置 pod 布局

可以控制具有特定资源的 Kubernetes 节点上的 pod 放置，以适应各种类型的工作负载要求。 例如, 你可能想要确保将存储池资源盒放置在具有更多存储的节点上, 或者将 SQL Server 主实例放置在 CPU 和内存资源较高的节点上。 在这种情况下，需首先构建具有不同类型硬件的异类 Kubernetes 群集，然后相应[分配节点标签](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/)。 部署大数据群集时，可在群集部署配置文件中，在池级别指定相同的标签。 然后，kubernetes 负责将与指定标签匹配的节点上的 pod 关联起来。 需要添加到 kubernetes 群集中节点的特定标签键是**mssql 群集范围内**的。 此标签本身的值可以是所选择的任何字符串。

下面的示例演示如何编辑自定义配置文件以包括 SQL Server 主实例、计算池、数据池 & 存储池的节点标签设置。 请注意，内置配置中没有 nodeLabel 键，因此需要手动编辑自定义配置文件或创建修补程序文件并将其应用于自定义配置文件。 SQL Server 的主实例 pod 将部署在一个节点上, 该节点包含具有值**bdc-Master**的标签**mssql-群集**。 计算池和数据池箱将部署在包含一个标签为**mssql-群集**的节点上, 其值为 " **bdc-sql**"。 存储池将部署在一个节点上, 在该节点上, 其值为 "bdc-**群集**-**存储**"。

在当前目录中创建名为“patch.json”的文件，其内容如下：

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "spec.resources.master.spec",
      "value": {
        "type": "Master",
        "replicas": 1,
        "endpoints": [
          {
            "name": "Master",
            "serviceType": "NodePort",
            "port": 31433
          }
        ],
        "settings": {
          "sql": {
            "hadr.enabled": "false"
          }
        },
        "nodeLabel": "bdc-master"
      }
    },
    {
      "op": "replace",
      "path": "spec.resources.compute-0.spec",
      "value": {
        "type": "Compute",
        "replicas": 1,
        "nodeLabel": "bdc-sql"
      }
    },
    {
      "op": "replace",
      "path": "spec.resources.data-0.spec",
      "value": {
        "type": "Data",
        "replicas": 2,
        "nodeLabel": "bdc-sql"
      }
    },
    {
      "op": "replace",
      "path": "spec.resources.storage-0.spec",
      "value": {
        "type": "Storage",
        "replicas": 3,
        "nodeLabel": "bdc-storage",
        "settings": {
          "spark": {
            "includeSpark": "true"
          }
        }
      }
    }
  ]
}
```

```bash
azdata bdc config patch --config-file custom/bdc.json --patch-file ./patch.json
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

- 更新**bdc**中存储池的池存储设置。
```json
{
  "patch": [
    {
      "op": "replace",
      "path": "spec.resources.storage-0.spec",
      "value": {
        "type": "Storage",
        "replicas": 2,
        "storage": {
          "data": {
            "size": "100Gi",
            "className": "myStorageClass",
            "accessMode": "ReadWriteOnce"
          },
          "logs": {
            "size": "32Gi",
            "className": "myStorageClass",
            "accessMode": "ReadWriteOnce"
          }
        }
      }
    }
  ]
}
```

- 更新**bdc**中存储池的 Spark 设置。
```json
{
  "patch": [
    {
      "op": "replace",
      "path": "spec.services.spark.settings",
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

- 创建包含两个实例的 spark 池。
```json
{
  "patch": [
    {
      "op": "add",
      "path": "spec.resources.spark-0",
      "value": {
        "metadata": {
          "kind": "Pool",
          "name": "default"
        },
        "spec": {
          "type": "Spark",
          "replicas": 2
        }
      }
    },
    {
      "op": "add",
      "path": "spec.services.spark.resources/-",
      "value": "spark-0"
    },
    {
      "op": "add",
      "path": "spec.services.hdfs.resources/-",
      "value": "spark-0"
    },
    {
      "op": "add",
      "path": "spec.services.spark.settings",
      "value": {
        "DriverMemory": "2g",
        "DriverCores": "1",
        "ExecutorInstances": "2",
        "ExecutorMemory": "2g",
        "ExecutorCores": "1"
      }
    }
  ]
}
```

> [!TIP]
> 有关部署配置文件的结构和用于更改该文件的选项的更多信息，请参阅[大数据群集的部署配置文件参考](reference-deployment-config.md)。

使用“azdata bdc config”命令来应用 json 修补程序文件中的更改。 下面的示例将**patch**文件应用到目标部署配置文件**自定义/bdc。**

```bash
azdata bdc config patch --config-file custom/bdc.json --patch-file ./patch.json
```

## <a name="disable-elasticsearch-to-run-in-privileged-mode"></a>禁止 ElasticSearch 在特权模式下运行
默认情况下, ElasticSearch 容器在大数据群集的特权模式下运行。 这是为了确保在容器初始化时, 容器具有足够的权限, 以便在 ElasticSearch 处理更多日志时, 对主机所需上的设置进行更新。 可以在[本文](https://www.elastic.co/guide/en/elasticsearch/reference/current/vm-max-map-count.html)中找到有关此主题的详细信息。 

若要禁用运行 ElasticSearch 的容器以便在特权模式下运行, 则必须更新**控件 json**中的 "**设置**" 部分, 并将 " **_map_count** " 的值指定为 " **-1**"。 下面是此部分的外观示例:
```json
"settings": {
    "ElasticSearch": {
        "vm.max_map_count": "-1"
      }
}
```

您可以手动编辑**控件 json**并将上述部分添加到**规范**中, 也可以创建如下所示的修补程序文件**elasticsearch** , 并使用**azdata** CLI 来修补**配置 json**文件:

```json
{
  "patch": [
    {
      "op": "replace",
      "path": "spec",
      "value": {
        "docker": {
            "registry": "mcr.microsoft.com",
            "repository": "mssql/bdc",
            "imageTag": "2019-RC1-ubuntu",
            "imagePullPolicy": "Always"
        },
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
        ],
        "settings": {
            "ElasticSearch": {
                "vm.max_map_count": "-1"
             }
        }
       }
    }
  ]
}
```

运行以下命令, 修补配置文件:
```
azdata bdc config patch --config-file control.json --patch-file elasticsearch-patch.json
```

> [!IMPORTANT]
> 建议在 Kubernetes 群集中的每个主机上手动手动更新**max_map_count**设置, 如[本文](https://www.elastic.co/guide/en/elasticsearch/reference/current/vm-max-map-count.html)中的说明。
## <a name="next-steps"></a>后续步骤

有关在大数据群集部署中使用配置文件的详细信息, 请参阅[如何[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]在 Kubernetes 上部署](deployment-guidance.md#configfile)。
