---
title: 使用 RStudio 从 sparklyr
titleSuffix: SQL Server big data clusters
description: 连接到使用 RStudio 从 sparklyr 的大数据群集。
author: jejiang
ms.author: jejiang
ms.reviewer: jroth
ms.date: 04/08/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 148e4942babafb35af2efe33eb427f9462f0a47e
ms.sourcegitcommit: 2e7686443a61b1a2cf4ca47d9ab1010b9e9b5188
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59291577"
---
# <a name="use-sparklyr-in-sql-server-big-data-cluster"></a>在 SQL Server 大数据群集中使用 sparklyr

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Sparklyr 适用于 Apache Spark 提供的 R 接口。 Sparklyr 是 R 开发人员使用 Spark 一种流行方式。 本文介绍如何在使用 RStudio 的 SQL Server 2019 大数据群集 （预览版） 中使用 sparklyr。

## <a name="prerequisites"></a>先决条件

- [部署 SQL Server 2019 大数据群集](quickstart-big-data-cluster-deploy.md)。

### <a name="install-rstudio-desktop"></a>安装 RStudio Desktop

安装和配置**RStudio Desktop**通过执行以下步骤：

1. 如果你在 Windows 客户端上运行[下载并安装 R 3.4.4](https://cran.rstudio.com/bin/windows/base/old/3.4.4)。

1. [下载并安装 RStudio Desktop](https://www.rstudio.com/products/rstudio/download/)。

1. 安装完成后，运行 RStudio Desktop 内的以下命令以安装所需的包：

   ```RStudio Desktop install.packages("DBI", repos = "https://cran.microsoft.com/snapshot/2019-01-01") install.packages("dplyr", repos = "https://cran.microsoft.com/snapshot/2019-01-01") install.packages("sparklyr", repos = "https://cran.microsoft.com/snapshot/2019-01-01")
   ```

## Connect to Spark in a big data cluster

You can use sparklyr to connect from a client to the big data cluster using Livy and the HDFS/Spark gateway. 

In RStudio, create an R script and connect to Spark as in the following example:

> [!TIP]
> For the `<USERNAME>` and `<PASSWORD>` values, use the username (such as root) and password you set during the big data cluster deployment. For the `<IP>` and `<PORT>` values, see the documentation on the [HDFS/Spark gateway](connect-to-big-data-cluster.md#hdfs).

```r
library(sparklyr)
library(dplyr)
library(DBI)

#Specify the Knox username and password
config <- livy_config(user = "<username>", password = "<password>")

httr::set_config(httr::config(ssl_verifypeer = 0L, ssl_verifyhost = 0L))

sc <- spark_connect(master = "https://<IP>:<PORT>/gateway/default/livy/v1",
                    method = "livy",
                    config = config)
```

## <a name="run-sparklyr-queries"></a>运行 sparklyr 查询

连接到 Spark 后，可以运行 sparklyr。 以下示例对使用 sparklyr 鸢尾花数据集执行查询：

```r
iris_tbl <- copy_to(sc, iris)

iris_count <- dbGetQuery(sc, "SELECT COUNT(*) FROM iris")

iris_count
```

## <a name="distributed-r-computations"></a>分布式的 R 计算

Sparklyr 的一项功能是能够[R 计算分布](https://spark.rstudio.com/guides/distributed-r/)与[spark_apply](https://spark.rstudio.com/reference/spark_apply/)。

由于大数据群集使用 Livy 连接，因此必须设置`packages = FALSE`对的调用中**spark_apply**。 有关详细信息，请参阅[Livy 部分](https://spark.rstudio.com/guides/distributed-r/#livy)sparklyr 文档上分布式 R 计算。 使用此设置，你只能使用传递给 R 代码中在 Spark 群集已安装的 R 包**spark_apply**。 下面的示例演示了此功能：

```r
iris_tbl %>% spark_apply(function(e) nrow(e), names = "nrow", group_by = "Species", packages = FALSE)
```

## <a name="next-steps"></a>后续步骤

有关大数据群集的详细信息，请参阅[什么是 SQL Server 2019 大数据群集](big-data-cluster-overview.md)。