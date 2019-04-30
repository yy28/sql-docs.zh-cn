---
title: 使用 curl 将数据加载到 HDFS |Microsoft Docs
titleSuffix: SQL Server big data clusters
description: 使用 curl 在 SQL Server 2019 大数据群集上将数据加载到 HDFS。
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 74e08c16e528c580bf78b3928a1aaf0c9b3eb069
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
ms.locfileid: "63472095"
---
# <a name="use-curl-to-load-data-into-hdfs-on-sql-server-big-data-clusters"></a>使用 curl 在 SQL Server 大数据群集上将数据加载到 HDFS

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

本文介绍如何使用**curl**将数据加载到 HDFS，SQL Server 2019 大数据群集 （预览版） 上。

## <a name="obtain-the-service-external-ip"></a>获取服务的外部 IP

在完成部署，并且其访问权限将经历 Knox 启动 WebHDFS。 通过名为的 Kubernetes 服务公开的 Knox 终结点**网关 svc 外部**。  若要创建要上传/下载文件的必要 WebHDFS URL，需要**网关 svc 外部**服务外部的 IP 地址和群集的名称。 可以获取**网关 svc 外部**服务外部的 IP 地址通过运行以下命令：

```bash
kubectl get service gateway-svc-external -n <cluster name> -o json | jq -r .status.loadBalancer.ingress[0].ip
```

> [!NOTE]
> `<cluster name>`以下是你提供在运行时群集的名称`mssqlctl cluster create --name <cluster name>`。

## <a name="construct-the-url-to-access-webhdfs"></a>构造用于访问 WebHDFS 的 URL

现在，您可以构造用于访问 WebHDFS，如下所示的 URL:

`https://<gateway-svc-external service external IP address>:30443/gateway/default/webhdfs/v1/`

例如：

`https://13.66.190.205:30443/gateway/default/webhdfs/v1/`

## <a name="list-a-file"></a>列出文件

下列表文件**hdfs: / / airlinedata**，使用以下 curl 命令：

```bash
curl -i -k -u root:root-password -X GET 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/airlinedata/?op=liststatus'
```

## <a name="put-a-local-file-into-hdfs"></a>将本地文件放置在 HDFS

若要将新文件放**test.csv**从本地目录更改为 airlinedata 目录，请使用以下 curl 命令 (**内容类型**参数是必需的):

```bash
curl -i -L -k -u root:root-password -X PUT 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/airlinedata/test.csv?op=create' -H 'Content-Type: application/octet-stream' -T 'test.csv'
```

## <a name="create-a-directory"></a>创建一个目录

若要创建一个目录**测试**下`hdfs:///`，使用以下命令：

```bash
curl -i -L -k -u root:root-password -X PUT 'https://<gateway-svc-external IP external address>:30443/gateway/default/webhdfs/v1/test?op=MKDIRS'
```

## <a name="next-steps"></a>后续步骤

有关 SQL Server 大数据群集的详细信息，请参阅[什么是 SQL Server 大数据群集？](big-data-cluster-overview.md)。
