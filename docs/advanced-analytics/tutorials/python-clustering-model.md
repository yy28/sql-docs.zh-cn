---
title: Python 教程：将用户分类
description: 本系列教程由四个部分组成，你将使用 K-Means 在 SQL 数据库中结合使用 Python 与 SQL Server 机器学习服务对客户进行群集。
ms.prod: sql
ms.technology: machine-learning
ms.devlang: python
ms.date: 12/17/2019
ms.topic: tutorial
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f5d1254c6b5c478c7bcad63da0902f21f4db70a9
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "75306583"
---
# <a name="tutorial-categorizing-customers-using-k-means-clustering-with-sql-server-machine-learning-services"></a>教程：配合使用 K-Means 群集和 SQL Server 机器学习服务对客户进行分类

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本系列教程由四个部分组成，引导你使用 Python 在 [SQL Server 机器学习服务](../what-is-sql-server-machine-learning.md)中开发和部署 K-Means 群集模型，以便对客户数据进行聚类分析。

在本系列的第一部分，设置本教程的先决条件，然后将示例数据集还原到一个 SQL 数据库。 在本系列的后续部分中，使用这些数据在 Python 中通过 SQL Server 机器学习服务来定型和部署聚类分析模型。

在本系列的第二和第三部分中，在 Azure Data Studio 笔记本中开发一些 Python 脚本，用于分析和准备数据以及定型机器学习模型。 然后，在第四部分中，使用存储过程在 SQL 数据库中运行这些 Python 脚本。

聚类分析可解释为将数据组织成组，其中一个组的成员在某些方面类似  。 对于本系列教程，假设你拥有一家零售企业。 你将使用 K-Means 算法在产品购买及退货的数据集中执行针对客户的聚类分析  。 通过对客户进行聚类分析，可以将特定组定为目标，更加高效地专注于市场营销工作。
K-Means 群集是一种无监督式学习算法，该算法根据相似性寻找数据中的规律  。

本文将指导如何进行以下操作：

> [!div class="checklist"]
> * 将示例数据库还原为一个 SQL Server 实例

[第二部分](python-clustering-model-prepare-data.md)介绍如何准备 SQL 数据库中的数据以执行聚类分析。

[第三部分](python-clustering-model-build.md)介绍如何在 Python 中创建和定型 K-Means 群集模型。

在[第四部分](python-clustering-model-deploy.md)中，你将了解如何在 SQL 数据库中创建存储过程，以便基于新数据在 Python 中执行聚类分析。

## <a name="prerequisites"></a>必备条件

* 支持 Python 语言的 [SQL Server 机器学习服务](../what-is-sql-server-machine-learning.md) - 按照 [Windows 安装指南](../install/sql-machine-learning-services-windows-install.md)或 [Linux 安装指南](https://docs.microsoft.com/sql/linux/sql-server-linux-setup-machine-learning?toc=%2fsql%2fadvanced-analytics%2ftoc.json&view=sql-server-linux-ver15)中的安装说明进行操作。

* [Azure Data Studio](../../azure-data-studio/what-is.md)。 你将使用 Azure Data Studio 中同时适用于 Python 和 SQL 的笔记本。 若要详细了解笔记本，请参阅[如何使用 Azure Data Studio 中的笔记本](../../azure-data-studio/sql-notebooks.md)。

  * Python - 也可以使用你自己的 Python IDE，如 Jupyter 笔记本或 [Visual Studio Code](https://code.visualstudio.com/docs)（具有 [Python 扩展](https://marketplace.visualstudio.com/items?itemName=ms-python.python)和 [mssql 扩展](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)）。
  * SQL - 也可以使用 [SQL Server Management Studio](../../ssms/sql-server-management-studio-ssms.md) (SSMS)。

* 附加 Python 包 - 在本教程系列中的示例所使用的 Python 包中，有些可能是你已经安装了的，有些可能是你尚未安装的。

  打开命令提示符  ，并更改为 Azure Data Studio 中使用的 Python 版本的安装路径。 例如，`cd %LocalAppData%\Programs\Python\Python37-32` 。 然后，运行下面的命令，以安装所有尚未安装的包。

  ```console
  pip install matplotlib
  pip install pandas
  pip install pyodbc
  pip install scipy
  pip install sklearn
  ```

## <a name="restore-the-sample-database"></a>还原示例数据库

本教程中使用的示例数据集已保存到 **.bak** 数据库备份文件，以供下载和使用。 此数据集派生自 [事务处理性能委员会 (TPC)](http://www.tpc.org/default.asp) 提供的 [tpcx-bb](http://www.tpc.org/tpcx-bb/default.asp) 数据集。

1. 下载 [tpcxbb_1gb.bak](https://sqlchoice.blob.core.windows.net/sqlchoice/static/tpcxbb_1gb.bak) 文件。

1. 使用以下详细信息，按 Azure Data Studio 中[从备份文件还原数据库](../../azure-data-studio/tutorial-backup-restore-sql-server.md#restore-a-database-from-a-backup-file)中的说明操作：

   * 从下载的 tpcxbb_1gb.bak 文件导入 
   * 将目标数据库命名为“tpcxbb_1gb”

1. 可以查询 dbo.customer 表验证数据库还原后数据集是否存在  ：

    ```sql
    USE tpcxbb_1gb;
    SELECT * FROM [dbo].[customer];
    ```

## <a name="clean-up-resources"></a>清理资源

如果不打算继续学习本教程，请从 SQL Server 中删除 tpcxbb_1gb 数据库。

## <a name="next-steps"></a>后续步骤

在本系列教程的第一部分中，你已完成以下步骤：

* 将示例数据库还原为一个 SQL Server 实例

若要为机器学习模型准备数据，按本系列教程的第二部分进行操作：

> [!div class="nextstepaction"]
> [教程：准备数据以通过 SQL Server 机器学习服务在 Python 中执行聚类分析](python-clustering-model-prepare-data.md)
