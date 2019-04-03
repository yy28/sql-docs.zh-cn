---
title: 使用 RStudio 从 sparklyr
titleSuffix: SQL Server big data clusters
description: 连接到使用 RStudio 从 sparklyr 的大数据群集。
author: jejiang
ms.author: jejiang
ms.reviewer: jroth
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 30b8ddccd01c0e8d9a4eac34f2f504b0d8971af6
ms.sourcegitcommit: 2de5446fbc57787f18a907dd5deb02a7831ec07d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/02/2019
ms.locfileid: "58860188"
---
# <a name="use-sparklyr-in-sql-server-big-data-cluster"></a>在 SQL Server 大数据群集中使用 Sparklyr

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Sparklyr 适用于 Apache Spark 提供的 R 接口。 Sparklyr 是 R 开发人员使用 Spark 的首选方法。 本文介绍如何在使用 RStudio 的 SQL Server 2019 大数据群集 （预览版） 中使用 sparklyr。

## <a name="prerequisites"></a>先决条件

- [部署 SQL Server 2019 大数据群集](quickstart-big-data-cluster-deploy.md)。
- [安装 RStudio](https://www.rstudio.com/)

## <a name="connect-to-spark-in-ss19-big-data-cluster"></a>连接到 SS19 大数据群集中的 spark

在 RStudio 中创建 RScript 并连接到 Spark，如下所示。 Spark 大数据群集连接通过 Livy，可以通过访问[HDFS/Spark 网关](connect-to-big-data-cluster.md#hdfs)。 对于身份验证，使用的用户名和密码在部署期间设置。

```r
library(sparklyr)
library(dplyr)
library(DBI)

#Specify the Knox username and password
config <- livy_config(user = "***root***", password = "****")

httr::set_config(httr::config(ssl_verifypeer = 0L))

sc <- spark_connect(master = "https://<IP>:<PORT>/gateway/default/livy/v1",
                    method = "livy",
                    config = config)
```

## <a name="run-sparklyr-queries"></a>运行 sparklyr 查询

连接到 Spark 后，可以运行 sparklyr。 以下示例对使用 sparklyr 鸢尾花数据集执行查询：

``` r
copy_to(sc, iris)

iris_count <- dbGetQuery(sc, "SELECT COUNT(*) FROM iris")

iris_count
```

## <a name="next-steps"></a>后续步骤

有关大数据群集的详细信息，请参阅[什么是 SQL Server 2019 大数据群集？](big-data-cluster-overview.md)。