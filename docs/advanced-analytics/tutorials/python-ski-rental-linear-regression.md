---
title: Python 教程：滑雪租赁（线性回归）
description: 在本教程中，您将在 SQL Server 机器学习服务中使用 Python 和线性回归来预测滑雪租赁的数量。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/03/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 718487ba55b2b8db8f16b59df5785cf78ff501f1
ms.sourcegitcommit: ecb19d0be87c38a283014dbc330adc2f1819a697
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2019
ms.locfileid: "70242505"
---
# <a name="python-tutorial-predict-ski-rental-with-linear-regression-in-sql-server-machine-learning-services"></a>Python 教程：SQL Server 中的线性回归预测 ski 租赁机器学习服务
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在此四部分的系列教程中，你将在[SQL Server 机器学习服务](../what-is-sql-server-machine-learning.md)中使用 Python 和线性回归来预测 ski 租金的数量。 本教程[在 Azure Data Studio 中使用 python 笔记本](../../azure-data-studio/sql-notebooks.md)，但你也可以使用自己的 python 集成开发环境（IDE）。

假设您拥有一个 ski 租赁企业，并且您想要预测您将在将来的某个日期的租赁数量。 此信息可帮助你准备好股票、员工和设施。

在本系列文章的第一部分中，你将设置必备组件。 在第二和第三部分中，你将在 Jupyter 笔记本中开发一些 Python 脚本，以便准备你的数据和训练机器学习模型。 然后，在第三部分中，你将使用 T-sql 存储过程在 SQL Server 中运行这些 Python 脚本。

本文将介绍如何执行以下操作：

> [!div class="checklist"]
> * 将示例数据库导入 SQL Server 

在[第二部分](python-ski-rental-linear-regression-prepare-data.md)中，你将了解如何将数据从 SQL Server 加载到 python 数据帧中，以及如何在 python 中准备数据。

在[第三部分](python-ski-rental-linear-regression-train-model.md)中，你将了解如何在 Python 中训练线性回归模型。

在[第四部分](python-ski-rental-linear-regression-deploy-model.md)中，你将了解如何将模型存储到 SQL Server，然后从你在第二和第三部分中开发的 Python 脚本中创建存储过程。 存储过程将在 SQL Server 中运行，以便基于新数据进行预测。

## <a name="prerequisites"></a>先决条件

* SQL Server 机器学习服务-有关如何安装机器学习服务的详细说明，请参阅[Windows 安装指南](../install/sql-machine-learning-services-windows-install.md)或[Linux 安装指南](../../linux/sql-server-linux-setup-machine-learning.md?toc=%2Fsql%2Fadvanced-analytics%2Ftoc.json)。

* Python IDE-本教程使用[Azure Data Studio](../../azure-data-studio/what-is.md)中的 Python 笔记本。 有关详细信息，请参阅[如何在 Azure Data Studio 中使用笔记本](../../azure-data-studio/sql-notebooks.md)。 

    你还可以使用自己的 Python IDE，例如 Jupyter 笔记本或使用[python 扩展](https://marketplace.visualstudio.com/items?itemName=ms-python.python)和[mssql 扩展](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)的[Visual Studio Code](https://code.visualstudio.com/docs) 。 

* [revoscalepy](../python/ref-py-revoscalepy.md)包- **revoscalepy**包包含在 SQL Server 机器学习服务中。 若要在客户端计算机上使用包，请参阅为[Python 开发设置数据科学客户端](../python/setup-python-client-tools-sql.md)，以便在本地安装此包。

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
    pip install pandas
    pip install sklearn
    pip install pickle
    ```

## <a name="restore-the-sample-database"></a>还原示例数据库

本教程中使用的示例数据集已保存到 **.bak**数据库备份文件，供你下载和使用。

1. 下载文件[TutorialDB](https://sqlchoice.blob.core.windows.net/sqlchoice/static/TutorialDB.bak)。

1. 使用以下详细信息，按照 Azure Data Studio 中的[备份文件还原数据库](../../azure-data-studio/tutorial-backup-restore-sql-server.md#restore-a-database-from-a-backup-file)中的说明操作：

   * 从下载的**TutorialDB**文件导入
   * 将目标数据库命名为 "TutorialDB"

1. 您可以通过查询**rental_data**表来验证数据集是否存在。

    ```sql
    USE TutorialDB;
    SELECT * FROM [dbo].[rental_data];
    ```

## <a name="next-steps"></a>后续步骤

在本系列教程的第一部分中，你已完成以下步骤：

* 已安装必备组件
* 将示例数据库导入 SQL Server

若要从 TutorialDB 数据库中准备数据，请遵循本教程系列的第二部分：

> [!div class="nextstepaction"]
> [Python 教程：准备数据以训练线性回归模型](python-ski-rental-linear-regression-prepare-data.md)