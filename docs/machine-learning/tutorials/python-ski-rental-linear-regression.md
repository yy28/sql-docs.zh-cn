---
title: Python 教程：雪橇租赁
description: 本教程系列由四个部分组成。在第三部分中，你将在 Python 中生成线性回归模型，以在 SQL Server 机器学习服务中预测雪橇租赁次数。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/02/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 8f07c056e903f1036bfba15398f7cf54a1985f2d
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/04/2020
ms.locfileid: "81116410"
---
# <a name="python-tutorial-predict-ski-rental-with-linear-regression-in-sql-server-machine-learning-services"></a>Python 教程：在 SQL Server 机器学习服务中使用线性回归来预测雪橇租赁
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在这个由四个部分组成的教程系列中，你将在 [SQL Server 机器学习服务](../what-is-sql-server-machine-learning.md)中使用 Python 和线性回归来预测雪橇租赁次数。 本教程使用 [Azure Data Studio 中的 Python Notebook](../../azure-data-studio/sql-notebooks.md)，你也可以使用自己的 Python 集成开发环境 (IDE)。

假设你有一家雪橇租赁公司，你希望预测未来某个日期的雪橇租赁次数。 此信息可帮助你准备好库存、人员和设施。

在本系列的第一部分，你将设置必备组件。 在第二和第三部分，你将在 Jupyter Notebook 中开发一些 Python 脚本，以准备数据并定型机器学习模型。 然后，在第四部分，你将使用 T-SQL 存储过程在 SQL Server 中运行这些 Python 脚本。

本文将指导如何进行以下操作：

> [!div class="checklist"]
> * 将示例数据库导入 SQL Server 

[第二部分](python-ski-rental-linear-regression-prepare-data.md)介绍如何将数据从 SQL Server 加载到 Python 数据帧，并在 Python 中准备数据。

[第三部分](python-ski-rental-linear-regression-train-model.md)介绍如何在 Python 中定型线性回归模型。

[第四部分](python-ski-rental-linear-regression-deploy-model.md)介绍如何将模型存储到 SQL Server，然后根据在第二和第三部分中开发的 Python 脚本来创建存储过程。 存储过程将在 SQL Server 中运行，以便基于新数据进行预测。

## <a name="prerequisites"></a>先决条件

* SQL Server 机器学习服务 — 有关如何安装机器学习服务的信息，请参阅 [Windows 安装指南](../install/sql-machine-learning-services-windows-install.md)或 [Linux 安装指南](../../linux/sql-server-linux-setup-machine-learning.md?toc=%2Fsql%2Fmachine-learning%2Ftoc.json)。

* Python IDE - 本教程在 [Azure Data Studio](../../azure-data-studio/what-is.md) 中使用 Python 笔记本。 有关详细信息，请参阅[如何使用 Azure Data Studio 中的笔记本](../../azure-data-studio/sql-notebooks.md)。 

    还可以使用自己的 Python IDE，例如 Jupyter 笔记本或具有 [Python 扩展](https://marketplace.visualstudio.com/items?itemName=ms-python.python)和 [mssql 扩展](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)的 [Visual Studio Code](https://code.visualstudio.com/docs)。 

* SQL 查询工具 - 本教程假定使用的是 [Azure Data Studio](../../azure-data-studio/what-is.md)。 也可以使用 [SQL Server Management Studio](../../ssms/sql-server-management-studio-ssms.md) (SSMS)。

* 附加 Python 包 - 在本教程系列中的示例所使用的以下 Python 包中，有些可能是默认未安装的：

  * pandas
  * pyodbc
  * sklearn

  若要安装这些包：
  1. 在 Azure Data Studio 中，选择“管理包”  。
  2. 在“管理包”  窗格中，选择“添加新包”  选项卡。
  3. 对于以下每个包，输入包名称，单击“搜索”  ，然后单击“安装”  。

  作为替代方法，你可以打开“命令提示符”  ，更改为在 Azure Data Studio 中使用的 Python 版本的安装路径（例如 `cd %LocalAppData%\Programs\Python\Python37-32`），然后针对每个包运行 `pip install`。

## <a name="restore-the-sample-database"></a>还原示例数据库

本教程中使用的示例数据库已保存到 .bak  数据库备份文件，以供下载和使用。

1. 下载文件 [TutorialDB.bak](https://sqlchoice.blob.core.windows.net/sqlchoice/static/TutorialDB.bak)。

1. 使用以下详细信息，按 Azure Data Studio 中[从备份文件还原数据库](../../azure-data-studio/tutorial-backup-restore-sql-server.md#restore-a-database-from-a-backup-file)中的说明操作：

   * 从下载的 **TutorialDB.bak** 文件中导入
   * 将目标数据库命名为“TutorialDB”

1. 可以通过查询 dbo.rental_data  表来验证是否存在还原的数据集：

   ```sql
   USE TutorialDB;
   SELECT * FROM [dbo].[rental_data];
   ```

通过运行以下 SQL 命令来启用外部脚本：

  ```sql
  sp_configure 'external scripts enabled', 1;
  RECONFIGURE WITH override;
  ```

## <a name="next-steps"></a>后续步骤

在本系列教程的第一部分中，你已完成以下步骤：

* 安装必备组件
* 将示例数据库导入 SQL Server

若要从 TutorialDB 数据库中准备数据，请按照本教程系列的第二部分进行操作：

> [!div class="nextstepaction"]
> [Python 教程：准备数据以定型线性回归模型](python-ski-rental-linear-regression-prepare-data.md)