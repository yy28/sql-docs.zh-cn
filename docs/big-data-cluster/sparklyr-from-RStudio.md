---
title: 使用 RStudio 从 sparklyr
titleSuffix: SQL Server 2019 big data clusters
description: 连接到使用 RStudio 从 sparklyr 的大数据群集。
author: jejiang
ms.author: jejiang
ms.reviewer: jroth
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 83980f9d08a3894b0fbf7871cf899483e06702c4
ms.sourcegitcommit: 2533383a7baa03b62430018a006a339c0bd69af2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57018353"
---
# <a name="use-sparklyr-in-sql-server-2019-big-data-cluster"></a>在 SQL Server 2019 大数据群集中使用 Sparklyr

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