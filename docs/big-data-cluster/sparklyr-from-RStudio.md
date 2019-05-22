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
ms.openlocfilehash: 8004146499bd8b17c7705f7558de075dfece5813
ms.sourcegitcommit: be09f0f3708f2e8eb9f6f44e632162709b4daff6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2019
ms.locfileid: "65994176"
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

   ```RStudioDesktop
   install.packages("DBI", repos = "https://cran.microsoft.com/snapshot/2019-01-01")
   install.packages("dplyr", repos = "https://cran.microsoft.com/snapshot/2019-01-01")
   install.packages("sparklyr", repos = "https://cran.microsoft.com/snapshot/2019-01-01")
   ```

## <a name="connect-to-spark-in-a-big-data-cluster"></a>大数据群集中连接到 Spark

Sparklyr 可用于从客户端连接到大数据群集使用 Livy 和 HDFS/Spark 网关。 

在 RStudio 中，创建一个 R 脚本并连接到 Spark，如以下示例所示：

> [!TIP]
> 有关`<USERNAME>`和`<PASSWORD>`值，请使用 （如根） 的用户名和密码在大数据群集部署过程中设置。 有关`<IP>`并`<PORT>`值，请参阅的文档[连接到大数据群集](connect-to-big-data-cluster.md)。

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
