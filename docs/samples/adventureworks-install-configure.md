---
title: 安装和配置 AdventureWorks 示例数据库-SQL |Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 06/19/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5b098d59bfbc30d5273e46ccef24b62fcb82dbf8
ms.sourcegitcommit: b91c0a7e981749758bd38e47a530d4e7bf1c5dd9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/10/2018
ms.locfileid: "40393352"
---
# <a name="adventureworks-installation-and-configuration"></a>AdventureWorks 安装和配置
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

AdventureWorks 下载链接和安装说明。 

## <a name="prerequisites"></a>必要條件

- [SQL Server](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016)或[Azure SQL 数据库](https://azure.microsoft.com/services/sql-database/)。 对于该示例的完整版本，使用 SQL Server 评估/开发人员/企业版。
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md)。 为获得最佳结果使用 2016 年 6 月发行版或更高版本。
 
## <a name="github-links"></a>Github 链接

- [所有 SQL 2014 2016年的 AdventureWorks 文件](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)
- [针对 SQL 2012 的所有 AdventureWorks 文件](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks2012)
- [所有 SQL 2008 和 2008R2 AdventureWorks 文件](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks2008r2)

## <a name="oltp-downloads"></a>OLTP 下载

可在下面找到 AdventureWorks OLTP 版本的直接链接：

- [AdventureWorks2017.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2017.bak)
- [AdventureWorks2016.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2016.bak)
- [AdventureWorks2014.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2014.bak)
- [AdventureWorks2012.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2012.bak)
- [AdventureWorks2008R2.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks2008r2/adventure-works-2008r2-oltp.bak)


## <a name="data-warehouse-downloads"></a>数据仓库下载

直接链接到 AdventureWorks 的数据仓库版本可在下文：

- [AdventureWorksDW2017.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2017.bak)
- [AdventureWorksDW2016.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2016.bak)
- [AdventureWorksDW2014.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2014.bak)
- [AdventureWorksDW2012.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2012.bak)
- [AdventureWorksDW2008R2.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks2008r2/adventure-works-2008-dw.bak)

## <a name="creation-scripts"></a>创建脚本
以下脚本可用于创建整个 AdventureWorks 数据库中的，而不考虑版本。 

- [AdventureWorks OLTP 脚本 Zip](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks-oltp-install-script.zip)
- [AdventureWorks DW 脚本 Zip](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW-data-warehouse-install-script.zip)

## <a name="install-to-sql-server"></a>到 SQL Server 安装

### <a name="restore-backup"></a>还原备份
请按照以下步骤来还原备份的数据库使用 SQL Server Management Studio。 

1. 打开 SQL Server Management Studio 并连接到目标 SQL Server 实例。
2. 右键单击**数据库**节点，然后选择**Restore Database**。
3. 选择**设备**，然后单击省略号 (**...**)
4. 在对话框**选择备份设备**，单击**添加**，导航到的服务器的文件系统中的数据库备份，并选择的备份。 单击“确定” 。
5. 如果需要更改数据的目标位置，并在日志文件，**文件**窗格。 请注意，它将数据和日志文件的不同驱动器上的最佳做法。
6. 单击“确定” 。 这将启动数据库还原。 完成后，必须安装 SQL Server 实例上的 AdventureWorks 数据库。

有关还原 SQL Server 数据库的详细信息，请参阅[使用 SSMS 将数据库备份还原](../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)。


### <a name="attach-a-datafile"></a>附加数据文件
请按照以下步骤来将附加使用 SQL Server Management Studio 为数据库数据文件。

1. 打开 SQL Server Management Studio 并连接到目标 SQL Server 实例。
2. 右键单击**数据库**节点，然后选择**附加**。
3. 选择**添加**并导航到。你想要附加的 MDF 文件。 
1. 选择该文件，然后单击**确定**。 
    1. 您选择的数据库应显示在底部窗口中。 如果列出该文件为"未找到"，选择省略号 (**...**) 旁边的文件名和更新的正确路径的路径。 
    1. 如果只有数据文件 (.mdf)，而不是日志文件 (.ldf)，然后突出显示在底部窗口.ldf 并选择**删除**。 这将创建新的日志文件。 
1. 选择**确定**可以附加的文件。 附加文件后，必须安装 SQL Server 实例上的 AdventureWorks 数据库。  

有关附加数据库文件的详细信息，请参阅[附加数据库](../relational-databases/databases/attach-a-database.md)。 

## <a name="install-to-azure-sql-database"></a>安装到 Azure SQL 数据库


如果你还没有 SQL Server 在 Azure 中，导航到[Azure 门户](https://portal.azure.com/)并创建新的 SQL 数据库。 过程中创建数据库，将创建的服务器。 记下的服务器。 请参阅[本教程](https://azure.microsoft.com/documentation/articles/sql-database-get-started/)在几分钟内创建数据库。

1. 连接到 Azure 门户。
1. 选择**创建资源**在左上角的导航窗格中。 
1. 选择**数据库**，然后选择**SQL 数据库**。 
1. 填写必需的信息。
1. 在中**选择源**字段中，选择**示例 (AdventureWorksLT)** 最新的 AdventureWorksLT 备份将备份还原。
1. 选择**创建**创建新 SQL 数据库，这是在 AdventureWorksLT 数据库的已还原的副本。 


## <a name="see-also"></a>另请参阅
[有关 SQL Server Management Studio 教程](../ssms/tutorials/tutorial-sql-server-management-studio.md)
[有关 SQL Server 数据库引擎教程](../relational-databases/database-engine-tutorials.md)
