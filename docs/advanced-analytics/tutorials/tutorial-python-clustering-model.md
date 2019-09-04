---
title: 教程：在 Python 中执行群集
description: 在此四部分的教程系列中，你将在 SQL 数据库中使用 Python 和 SQL Server 机器学习服务来执行客户群集。
ms.prod: sql
ms.technology: machine-learning
ms.devlang: python
ms.date: 08/30/2019
ms.topic: tutorial
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 595652a2bfa7392d3b4f900082f33cc589631147
ms.sourcegitcommit: ecb19d0be87c38a283014dbc330adc2f1819a697
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2019
ms.locfileid: "70238665"
---
# <a name="tutorial-perform-clustering-in-python-with-sql-server-machine-learning-services"></a>教程：在 Python 中执行群集 SQL Server 机器学习服务

在此四部分的教程系列中，你将使用 Python 在[SQL Server 机器学习服务](../what-is-sql-server-machine-learning.md)中开发和部署 K 平均值聚类分析模型，以对客户数据进行分类。

在此系列的第一部分中，你将设置本教程的先决条件，然后将示例数据集导入到 SQL 数据库。 稍后在本系列中，你将使用此数据，通过 SQL Server 机器学习服务在 Python 中训练和部署群集模型。

在此系列的第二和第三部分中，您将在 Azure Data Studio 笔记本中开发一些 Python 脚本，用于分析和准备您的数据并训练机器学习模型。 然后，在第四部分中，将使用存储过程在 SQL 数据库中运行这些 Python 脚本。

可以将*聚类分析*为将数据组织成组，其中组的成员在某种程度上类似。 对于本系列教程，假设你拥有零售业务。 您将使用**K 平均值**算法在产品购买的数据集中执行客户的聚类分析，并返回。 通过对客户进行群集化，你可以通过以特定组为目标，更有效地集中市场营销工作。
K 平均值聚类分析是一种*无人监督学习*算法，用于根据相似性查找数据中的模式。

本文将介绍如何执行以下操作：

> [!div class="checklist"]
> * 将示例数据库导入 SQL Server 实例

在[第二部分](tutorial-python-clustering-model-prepare-data.md)中，你将了解如何从 SQL 数据库准备要执行群集的数据。

在[第三部分](tutorial-python-clustering-model-build.md)中，你将了解如何在 Python 中创建和训练 K 平均值聚类分析模型。

在[第四部分](tutorial-python-clustering-model-deploy.md)中，你将了解如何在 SQL 数据库中创建一个存储过程，该存储过程可基于新数据在 Python 中执行群集操作。

## <a name="prerequisites"></a>先决条件

* 具有 Python 语言选项[SQL Server 机器学习服务](../what-is-sql-server-machine-learning.md)-按照[Windows 安装指南](../install/sql-machine-learning-services-windows-install.md)或[Linux 安装指南](https://docs.microsoft.com/sql/linux/sql-server-linux-setup-machine-learning?toc=%2fsql%2fadvanced-analytics%2ftoc.json&view=sql-server-linux-ver15)中的安装说明进行操作。

* Python IDE-本教程使用[Azure Data Studio](../../azure-data-studio/what-is.md)中的 Python 笔记本。 有关详细信息，请参阅[如何在 Azure Data Studio 中使用笔记本](../../azure-data-studio/sql-notebooks.md)。 你还可以使用自己的 Python IDE，例如 Jupyter 笔记本或使用[python 扩展](https://marketplace.visualstudio.com/items?itemName=ms-python.python)和[mssql 扩展](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)的[Visual Studio Code](https://code.visualstudio.com/docs) 。

* [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package)包- **revoscalepy**包包含在 SQL Server 机器学习服务中。 若要在客户端计算机上使用包，请参阅为[Python 开发设置数据科学客户端](../python/setup-python-client-tools-sql.md)，以便在本地安装此包。

  如果在 Azure Data Studio 中使用 Python 笔记本，请按照以下附加步骤使用**revoscalepy**：

  1. 打开 Azure Data Studio
  1. 从 "**文件**" 菜单中选择 "**首选项**"，然后选择 "**设置**"
  1. 展开**扩展**并选择**笔记本配置**
  1. 在 " **Python 路径**" 下，输入安装库的路径（例如`C:\path-to-python-for-mls`）
  1. 请确保已选中 "**使用现有 Python** "
  1. 重新启动 Azure Data Studio

  如果使用的是不同的 Python IDE，请对 IDE 执行类似的步骤。

* SQL 查询工具-本教程假定你使用的是[Azure Data Studio](../../azure-data-studio/what-is.md)。 你还可以使用[SQL Server Management Studio](../../ssms/sql-server-management-studio-ssms.md) （SSMS）。

* 其他 Python 包-本系列教程中的示例使用了你可能已安装或可能未安装的 Python 包。 如有必要，请使用以下**pip**命令安装这些包。

  ```console
  pip install matplotlib
  pip install scipy
  pip install sklearn
  ```

## <a name="import-the-sample-database"></a>导入示例数据库

本教程中使用的示例数据集已保存到 **.bak**数据库备份文件，供你下载和使用。 此数据集派生自[事务处理性能委员会（TPC）](http://www.tpc.org/default.asp)提供的[tpcx-bb](http://www.tpc.org/tpcx-bb/default.asp)数据集。

1. 将文件[tpcxbb_1gb](https://sqlchoice.blob.core.windows.net/sqlchoice/static/tpcxbb_1gb.bak)下载到 SQL Server 备份文件夹。 对于默认数据库实例，文件夹为：

   `C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\Backup\`

1. 打开 Azure Data Studio，连接到 SQL Server 实例，然后打开一个新的查询窗口。

1. 运行以下命令来还原数据库。

   ```sql
   USE master;
   GO

   RESTORE DATABASE tpcxbb_1gb
   FROM DISK = 'C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\Backup\tpcxbb_1gb.bak'
   WITH MOVE 'tpcxbb_1gb' TO 'C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\DATA\tpcxbb_1gb.mdf'
      , MOVE 'tpcxbb_1gb_log' TO 'C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\DATA\tpcxbb_1gb.ldf';
   GO
   ```

## <a name="clean-up-resources"></a>清理资源

如果不打算继续学习本教程，请从 SQL Server 中删除 tpcxbb_1gb 数据库。

## <a name="next-steps"></a>后续步骤

在本系列教程的第一部分中，你已完成以下步骤：

* 将示例数据库导入 SQL Server 实例

若要为机器学习模型准备数据，请遵循本教程系列的第二部分：

> [!div class="nextstepaction"]
> [教程：准备数据以在 Python 中执行群集 SQL Server 机器学习服务](tutorial-python-clustering-model-prepare-data.md)
