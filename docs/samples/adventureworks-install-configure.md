---
title: 安装和配置 AdventureWorks 示例数据库
description: 按照这些说明下载和安装 AdventureWorks 示例数据库与 SQL 服务器管理工作室或 Azure SQL 数据库中。
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.date: 06/19/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: 7fa3d199450750a444f2b67ae3e4583549d449b9
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "81484566"
---
# <a name="adventureworks-installation-and-configuration"></a>AdventureWorks 的安装和配置
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

AdventureWorks 下载链接和安装说明。 

## <a name="prerequisites"></a>先决条件

- [SQL 服务器](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)或[Azure SQL 数据库](https://azure.microsoft.com/services/sql-database/)。 对于示例的完整版本，请使用 SQL 服务器评估/开发人员/企业版。
- [SQL 服务器管理工作室](../ssms/download-sql-server-management-studio-ssms.md)。 为获得最佳效果，请使用 2016 年 6 月版本或更高版本。
 
## <a name="oltp-downloads"></a>OLTP 下载

直接链接到的OLTP版本的冒险工厂可以找到如下：

- [冒险工厂2017.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2017.bak)
- [冒险工厂2016.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2016.bak)
- [冒险工厂2014.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2014.bak)
- [冒险工厂2012.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2012.bak)
- [冒险工厂2008R2.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks2008r2/adventure-works-2008r2-oltp.bak)


## <a name="data-warehouse-downloads"></a>数据仓库下载

指向 AdventureWorks 的数据仓库版本的直接链接，如下所示：

- [冒险工厂DW2017.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2017.bak)
- [冒险工厂DW2016.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2016.bak)
- [冒险工厂DW2014.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2014.bak)
- [冒险工厂DW2012.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2012.bak)
- [冒险工厂DW2008R2.bak](https://github.com/microsoft/sql-server-samples/releases/download/adventureworks2008r2/adventure-works-2008r2-dw.bak)

## <a name="creation-scripts"></a>创建脚本
以下脚本可用于创建整个 AdventureWorks 数据库，而不考虑版本。 

- [冒险工厂OLTP脚本Zip](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks-oltp-install-script.zip)
- [冒险工厂 DW 脚本 Zip](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW-data-warehouse-install-script.zip)

## <a name="github-links"></a>GitHub 链接

- [SQL 2014 - 2016 的所有 AdventureWorks 文件](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)
- [SQL 2012 的所有 AdventureWorks 文件](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks2012)
- [SQL 2008 和 2008R2 的所有 AdventureWorks 文件](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks2008r2)

## <a name="install-to-sql-server"></a>安装到 SQL 服务器

### <a name="restore-backup"></a>还原备份
按照以下步骤使用 SQL 服务器管理工作室还原数据库的备份。 

1. 打开 SQL 服务器管理工作室并连接到目标 SQL Server 实例。
2. 右键单击**数据库**节点，然后选择 **"还原数据库**"。
3. 选择 **"设备"** 并单击椭圆 （**...**）
4. 在对话框中选择**备份设备**，单击"**添加**"，导航到服务器文件系统中的数据库备份，然后选择备份。 单击“确定”。 
5. 如果需要，请更改"**文件"** 窗格中数据和日志文件的目标位置。 请注意，最佳做法是将数据和日志文件放在不同的驱动器上。
6. 单击“确定”。  这将启动数据库还原。 完成后，您将在 SQL Server 实例上安装 AdventureWorks 数据库。

有关还原 SQL Server 数据库的详细信息，请参阅[使用 SSMS 还原数据库备份](../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)。


### <a name="attach-a-datafile"></a>附加数据文件
按照以下步骤使用 SQL 服务器管理工作室附加数据库的数据文件。

1. 打开 SQL 服务器管理工作室并连接到目标 SQL Server 实例。
2. 右键单击 **"数据库"** 节点，然后选择 **"附加**"。
3. 选择 **"添加**并导航到 "。要附加的 MDF 文件。 
1. 选择该文件，并单击“确定”。**** 
    1. 您选择的数据库应显示在底部窗口中。 如果文件列为"未找到"，请选择文件名旁边的省略号 （**...），** 并将路径更新为正确的路径。 
    1. 如果只有数据文件 （.mdf），而不是日志文件 （.ldf），则突出显示底部窗口中的 .ldf 并选择 **"删除**"。 这将创建新的日志文件。 
1. 选择 **"确定"** 以附加文件。 附加文件后，您将在 SQL Server 实例上安装 AdventureWorks 数据库。  

有关附加数据库文件的详细信息，请参阅[附加数据库](../relational-databases/databases/attach-a-database.md)。 

## <a name="install-to-azure-sql-database"></a>安装到 Azure SQL 数据库


如果 Azure 中尚未有 SQL 服务器，请导航到[Azure 门户](https://portal.azure.com/)并创建新的 SQL 数据库。 在创建数据库的过程中，您将创建一个服务器。 记下服务器。 请参阅[本教程](https://azure.microsoft.com/documentation/articles/sql-database-get-started/)，在几分钟内创建数据库。

1. 连接到 Azure 门户。
1. 选择 **"在**导航窗格左上角创建资源"。 
1. 选择“数据库”，然后选择“SQL 数据库”********。 
1. 填写必需的信息。
1. 在 **"选择源**"字段中，选择 **"示例"（AdventureWorksLT）** 以恢复最新 AdventureWorksLT 备份的备份。
1. 选择 **"创建**"以创建新的 SQL 数据库，该数据库是 AdventureWorksLT 数据库的还原副本。 


## <a name="see-also"></a>请参阅
[SQL 服务器管理工作室教程](../ssms/tutorials/tutorial-sql-server-management-studio.md)   
[SQL Server 数据库引擎教程](../relational-databases/database-engine-tutorials.md)
