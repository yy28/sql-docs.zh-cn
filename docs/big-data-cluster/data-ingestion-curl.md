---
title: 使用 curl 在 SQL Server 2019 大数据群集上将数据加载到 HDFS |Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/07/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: seodec18
ms.openlocfilehash: 890c323434c17bb66cd9a67aac872a5580cb2ddf
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2018
ms.locfileid: "53201616"
---
# <a name="use-curl-to-load-data-into-hdfs-on-sql-server-2019-big-data-clusters"></a>使用 curl 在 SQL Server 2019 大数据群集上将数据加载到 HDFS

本文介绍如何使用**curl**将数据加载到 HDFS，SQL Server 2019 大数据群集 （预览版） 上。

## <a name="obtain-the-service-external-ip"></a>获取服务的外部 IP

在完成部署，并且其访问权限将经历 Knox 启动 WebHDFS。 通过 Kubernetes 服务公开的 Knox 终结点 （适用于暂时） 调用**服务-安全性-l b**。若要创建将需要使用 CURL 上传/下载文件将需要的 WebHDFS URL**服务-安全性-l b**服务外部的 IP 地址和群集的名称。 可以通过运行以下命令来获取服务-安全性-l b 服务外部 IP 地址：

```bash
kubectl get service service-security-lb -n <cluster name> -o json | jq -r .status.loadBalancer.ingress[0].ip
```

> [!NOTE]
> `<cluster name>`以下是运行 mssqlctl 时提供群集的名称创建群集`<cluster name>`。

## <a name="construct-the-url-to-access-webhdfs"></a>构造用于访问 WebHDFS 的 URL

现在，您可以构造用于访问 WebHDFS，如下所示的 URL:

`https://<service-security-lb service external IP address>:30433/gateway/default/webhdfs/v1/`

例如：

`https://13.66.190.205:30443/gateway/default/webhdfs/v1/`

## <a name="list-a-file"></a>列出文件

下列表文件**hdfs: / / airlinedata**使用以下 curl 命令：

```bash
curl -i -k -u root:root-password -X GET 'https://<service-security-lb IP external address>:30443/gateway/default/webhdfs/v1/airlinedata/?op=liststatus'
```

## <a name="put-a-local-file-into-hdfs"></a>将本地文件放置在 HDFS

若要将新文件放**test.csv**从本地目录更改为 airlinedata 目录 (**内容类型**参数是必需的) 使用以下 curl 命令：

```bash
curl -i -L -k -u root:root-password -X PUT 'https://<service-security-lb IP external address>:30443/gateway/default/webhdfs/v1/airlinedata/test.csv?op=create' -H 'Content-Type: application/octet-stream' -T 'test.csv'
```

## <a name="create-a-directory"></a>创建一个目录

若要创建一个目录**测试**下`hdfs:///`使用以下命令：

```bash
curl -i -L -k -u root:root-password -X PUT 'https://<service-security-lb IP external address>:30443/gateway/default/webhdfs/v1/test?op=MKDIRS'
```

## <a name="next-steps"></a>后续步骤

有关 SQL Server 大数据群集的详细信息，请参阅[什么是 SQL Server 大数据群集？](big-data-cluster-overview.md)。