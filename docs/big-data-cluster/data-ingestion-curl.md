---
title: 使用 curl 将数据加载到 HDFS |Microsoft Docs
titleSuffix: SQL Server big data clusters
description: 使用卷将数据加载到 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]上的 HDFS 中。
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: c65ce7fb6752240f0dd23a6dab195539146e7933
ms.sourcegitcommit: 4fb6bc7c81a692a2df706df063d36afad42816af
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/29/2019
ms.locfileid: "73049878"
---
# <a name="use-curl-to-load-data-into-hdfs-on-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>使用卷将数据加载到 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] 上的 HDFS

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文介绍如何使用**卷**将数据加载到 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] （预览版）上的 HDFS 中。

## <a id="prereqs"></a> Prerequisites

- [将示例数据加载到大数据群集中](tutorial-load-sample-data.md)

## <a name="obtain-the-service-external-ip"></a>获取服务外部 IP

WebHDFS 在部署完成后启动，其访问通过 Knox 进行。 Knox 终结点通过名为“gateway-svc-external”的 Kubernetes 服务公开。  要创建必需的 WebHDFS URL 来上传/下载文件，需要 gateway-svc-external 服务外部 IP 地址和大数据群集的名称。 可以通过运行以下命令获取 gateway-svc-external 服务外部 IP 地址：

```bash
kubectl get service gateway-svc-external -n <big data cluster name> -o json | jq -r .status.loadBalancer.ingress[0].ip
```

> [!NOTE]
> 这里的 `<big data cluster name>` 是在部署配置文件中指定的群集的名称。 默认名称为`mssql-cluster`。

## <a name="construct-the-url-to-access-webhdfs"></a>构造用于访问 WebHDFS 的 URL

现在，可以按如下方式构造用于访问 WebHDFS 的 URL：

`https://<gateway-svc-external service external IP address>:30443/gateway/default/webhdfs/v1/`

例如：

`https://13.66.190.205:30443/gateway/default/webhdfs/v1/`

## <a name="list-a-file"></a>列出文件

若要列出**hdfs:///product_review_data**下的文件，请使用以下卷命令：

```bash
curl -i -k -u root:root-password -X GET 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/product_review_data/?op=liststatus'
```

## <a name="put-a-local-file-into-hdfs"></a>将本地文件放入 HDFS

若要将新的**文件 product_review_data**从本地目录保存到文件目录，请使用以下卷曲命令（ **content-type**参数是必需的）：

```bash
curl -i -L -k -u root:root-password -X PUT 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/product_review_data/test.csv?op=create' -H 'Content-Type: application/octet-stream' -T 'test.csv'
```

## <a name="create-a-directory"></a>创建目录

要在 `hdfs:///` 下创建目录测试，请使用以下命令：

```bash
curl -i -L -k -u root:root-password -X PUT 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/test?op=MKDIRS'
```

## <a name="next-steps"></a>后续步骤

有关 SQL Server 大数据群集的更多详细信息，请参阅[什么是 SQL Server 大数据群集？](big-data-cluster-overview.md)。
