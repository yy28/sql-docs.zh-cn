---
title: 安装 & 配置 AdventureWorks 示例数据库
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.date: 06/19/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: 0d9f6842ebe5e7d6ee923eef17f491f0cb7ef6ec
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056743"
---
# <a name="adventureworks-installation-and-configuration"></a>AdventureWorks 安装和配置
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

AdventureWorks 下载链接和安装说明。 

## <a name="prerequisites"></a>Prerequisites

- [SQL Server](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)或[Azure SQL 数据库](https://azure.microsoft.com/services/sql-database/)。 有关该示例的完整版本，请使用 SQL Server Evaluation/开发人员/企业版。
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md)。 为获得最佳结果，请使用2016年6月版或更高版本。
 
## <a name="github-links"></a>Github 链接

- [适用于 SQL 2014 的所有 AdventureWorks 文件-2016](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)
- [适用于 SQL 2012 的所有 AdventureWorks 文件](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks2012)
- [适用于 SQL 2008 和2008R2 的所有 AdventureWorks 文件](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks2008r2)

## <a name="oltp-downloads"></a>OLTP 下载

可在下面找到 AdventureWorks 的 OLTP 版本的直接链接：

- [AdventureWorks2017.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2017.bak)
- [AdventureWorks2016.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2016.bak)
- [AdventureWorks2014.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2014.bak)
- [AdventureWorks2012.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2012.bak)
- [AdventureWorks2008R2.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks2008r2/adventure-works-2008r2-oltp.bak)


## <a name="data-warehouse-downloads"></a>数据仓库下载

可在下面找到 AdventureWorks 数据仓库版本的直接链接：

- [AdventureWorksDW2017.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2017.bak)
- [AdventureWorksDW2016.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2016.bak)
- [AdventureWorksDW2014.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2014.bak)
- [AdventureWorksDW2012.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2012.bak)
- [AdventureWorksDW2008R2.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks2008r2/adventure-works-2008-dw.bak)

## <a name="creation-scripts"></a>创建脚本
可以使用以下脚本创建整个 AdventureWorks 数据库，而不考虑版本。 

- [AdventureWorks OLTP 脚本 Zip](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks-oltp-install-script.zip)
- [AdventureWorks DW 脚本 Zip](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW-data-warehouse-install-script.zip)

## <a name="install-to-sql-server"></a>安装到 SQL Server

### <a name="restore-backup"></a>还原备份
按照以下步骤使用 SQL Server Management Studio 还原数据库的备份。 

1. 打开 SQL Server Management Studio，然后连接到目标 SQL Server 实例。
2. 右键单击 "**数据库**" 节点，然后选择 "**还原数据库**"。
3. 选择 "**设备**"，然后单击省略号（ **...** ）
4. 在对话框中**选择 "备份设备**"，单击 "**添加**"，导航到服务器文件系统中的数据库备份，并选择备份。 单击“确定”。
5. 如果需要，在 "**文件**" 窗格中更改数据文件和日志文件的目标位置。 请注意，最佳做法是将数据和日志文件放在不同的驱动器上。
6. 单击“确定”。 这将启动数据库还原。 完成后，会在 SQL Server 实例上安装 AdventureWorks 数据库。

有关还原 SQL Server 数据库的详细信息，请参阅[使用 SSMS 还原数据库备份](../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)。


### <a name="attach-a-datafile"></a>附加数据文件
按照以下步骤使用 SQL Server Management Studio 附加数据库的数据文件。

1. 打开 SQL Server Management Studio，然后连接到目标 SQL Server 实例。
2. 右键单击 "**数据库**" 节点，然后选择 "**附加**"。
3. 选择 "**添加**" 并导航到。要附加的 .MDF 文件。 
1. 选择该文件，然后单击 **"确定"** 。 
    1. 所选数据库应显示在下窗口中。 如果文件被列为 "未找到"，请选择文件名旁边的省略号（ **...** ），并将路径更新为正确的路径。 
    1. 如果只有数据文件（.mdf），而不是日志文件（.ldf），则在底部窗口中突出显示 .ldf，然后选择 "**删除**"。 这将创建一个新的日志文件。 
1. 选择 **"确定"** 以附加文件。 附加文件后，会在 SQL Server 实例上安装 AdventureWorks 数据库。  

有关附加数据库文件的详细信息，请参阅[Attach a database](../relational-databases/databases/attach-a-database.md)。 

## <a name="install-to-azure-sql-database"></a>安装到 Azure SQL 数据库


如果你尚未在 Azure 中安装 SQL Server，请导航到[Azure 门户](https://portal.azure.com/)并创建新的 SQL 数据库。 在创建数据库的过程中，您将创建一个服务器。 记下服务器。 请参阅[此教程](https://azure.microsoft.com/documentation/articles/sql-database-get-started/)，在几分钟内创建数据库。

1. 连接到 Azure 门户。
1. 选择导航窗格左上角的 "**创建资源**"。 
1. 选择 "**数据库**"，然后选择 " **SQL 数据库**"。 
1. 填写必需的信息。
1. 在 "**选择源**" 字段中，选择 "**示例（AdventureWorksLT）** "，还原最新 AdventureWorksLT 备份的备份。
1. 选择 "**创建**" 以创建新的 SQL 数据库，这是 AdventureWorksLT 数据库的还原副本。 


## <a name="see-also"></a>另请参阅
[SQL Server Management Studio  教程](../ssms/tutorials/tutorial-sql-server-management-studio.md)  
[SQL Server 数据库引擎教程](../relational-databases/database-engine-tutorials.md)
