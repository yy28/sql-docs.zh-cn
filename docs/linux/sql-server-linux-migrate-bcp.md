---
title: 大容量数据复制到 Linux 上的 SQL Server |Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 01/30/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 7b93d0d7-7946-4b78-b33a-57d6307cdfa9
ms.openlocfilehash: 506d98acd28b38d0ce8867f96229632a306ae680
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47812146"
---
# <a name="bulk-copy-data-with-bcp-to-sql-server-on-linux"></a>使用 bcp 将数据批量复制到 Linux 上的 SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文介绍如何使用[bcp](../tools/bcp-utility.md)到 Linux 上的 SQL Server 实例和用户指定格式的数据文件之间大容量复制数据的命令行实用程序。

可以使用`bcp`大量的行导入 SQL Server 表，或将数据从 SQL Server 表导出到数据文件。 除非与 queryout 选项一起使用时`bcp`不需要了解 TRANSACT-SQL。 `bcp`命令行实用程序适用于 Microsoft SQL Server 在本地运行或在云中、 在 Linux、 Windows 或 Docker 和 Azure SQL 数据库和 Azure SQL 数据仓库中。

本文介绍如何：
- 数据导入到表使用`bcp in`命令
- 从表使用导出数据`bcp out`命令

## <a name="install-the-sql-server-command-line-tools"></a>安装 SQL Server 命令行工具

`bcp` 是 SQL Server 命令行工具进行，不会自动安装用于 Linux 上的 SQL Server 的一部分。 如果 Linux 计算机尚未安装 SQL Server 命令行工具，则必须安装它们。 有关如何安装这些工具的详细信息，请从以下列表中选择 Linux 分发版：

- [Red Hat Enterprise Linux (RHEL)](sql-server-linux-setup-tools.md#RHEL)
- [Ubuntu](sql-server-linux-setup-tools.md#ubuntu)
- [SUSE Linux Enterprise Server (SLES)](sql-server-linux-setup-tools.md#SLES)

## <a name="import-data-with-bcp"></a>使用 bcp 导入数据

在本教程中，示例数据库和表创建的本地 SQL Server 实例上 (**localhost**)，然后使用`bcp`将加载到从磁盘上的文本文件的示例表。

### <a name="create-a-sample-database-and-table"></a>创建示例数据库和表

让我们首先使用在本教程的其余部分使用一个简单表创建示例数据库。

1. 在 Linux 框中，打开命令终端。

2. 复制并粘贴到终端窗口中的以下命令。 这些命令使用**sqlcmd**命令行实用工具创建示例数据库 (**BcpSampleDB**) 和一个表 (**TestEmployees**) 上的本地 SQL Server 实例 (**localhost**)。 请记得替换`username`和`<your_password>`根据需要运行命令前。

创建数据库**BcpSampleDB**:
```bash 
sqlcmd -S localhost -U sa -P <your_password> -Q "CREATE DATABASE BcpSampleDB;"
```
创建表**TestEmployees**数据库中**BcpSampleDB**:
```bash 
sqlcmd -S localhost -U sa -P <your_password> -d BcpSampleDB -Q "CREATE TABLE TestEmployees (Id INT IDENTITY(1,1) NOT NULL PRIMARY KEY, Name NVARCHAR(50), Location NVARCHAR(50));"
```
### <a name="create-the-source-data-file"></a>创建源数据文件
复制并粘贴到终端窗口下面的命令。 我们使用内置`cat`命令，创建具有三条记录的示例文本数据文件作为主目录中将该文件 **~/test_data.txt**。 记录中的字段用逗号分隔。

```bash
cat > ~/test_data.txt << EOF
1,Jared,Australia
2,Nikita,India
3,Tom,Germany
EOF
```

你可以验证数据文件已正确创建，可以通过在终端窗口中运行以下命令：
```bash 
cat ~/test_data.txt
```

终端窗口中应该会显示以下内容：
```bash
1,Jared,Australia
2,Nikita,India
3,Tom,Germany
```

### <a name="import-data-from-the-source-data-file"></a>从源数据文件导入数据
复制并粘贴到终端窗口中的以下命令。 此命令使用`bcp`若要连接到本地 SQL Server 实例 (**localhost**) 和从数据文件导入数据 (**~/test_data.txt**) 到表 (**TestEmployees**) 在数据库中 (**BcpSampleDB**)。 请记得替换用户名和`<your_password>`根据需要运行命令前。

```bash 
bcp TestEmployees in ~/test_data.txt -S localhost -U sa -P <your_password> -d BcpSampleDB -c -t  ','
```

下面是我们使用的命令行参数的简要概述`bcp`在此示例中：
- `-S`： 指定要连接到 SQL Server 实例
- `-U`： 指定 ID 用于连接到 SQL Server 的登录名
- `-P`： 指定登录 ID 的密码
- `-d`： 指定要连接到的数据库
- `-c`： 使用字符数据类型进行操作
- `-t`： 指定字段终止符。 我们将使用`comma`作为我们的数据文件中的记录的字段终止符

> [!NOTE]
> 本示例中不指定自定义行终止符。 文本数据文件中的行已正确结尾`newline`时，我们使用`cat`命令之前创建数据文件。

你可以验证数据通过在终端窗口中运行以下命令已成功导入。 请记得替换`username`和`<your_password>`根据需要运行此命令之前。
```bash 
sqlcmd -S localhost -d BcpSampleDB -U sa -P <your_password> -I -Q "SELECT * FROM TestEmployees;"
```

应该会显示以下结果：
```bash
Id          Name                Location
----------- ------------------- -------------------
          1 Jared               Australia
          2 Nikita              India
          3 Tom                 Germany

(3 rows affected)
```

## <a name="export-data-with-bcp"></a>使用 bcp 导出数据

在本教程中，您使用`bcp`将数据导出到新的数据文件之前创建的示例表中。

复制并粘贴到终端窗口中的以下命令。 这些命令使用`bcp`命令行实用程序将从表导出数据**TestEmployees**数据库中**BcpSampleDB**到名为的新数据文件 **~/test_export.txt**.  请记得替换用户名和`<your_password>`根据需要运行此命令之前。

```bash 
bcp TestEmployees out ~/test_export.txt -S localhost -U sa -P <your_password> -d BcpSampleDB -c -t ','
```

你可以验证数据已正确导出，可以通过在终端窗口中运行以下命令：
```bash 
cat ~/test_export.txt
```

终端窗口中应该会显示以下内容：
```
1,Jared,Australia
2,Nikita,India
3,Tom,Germany
```

## <a name="see-also"></a>另请参阅
- [bcp 实用工具](../tools/bcp-utility.md)
- [在使用 bcp 时兼容性的数据格式](../relational-databases/import-export/specify-data-formats-for-compatibility-when-using-bcp-sql-server.md)
- [使用 BULK INSERT 批量导入数据](../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)
- [BULK INSERT (Transact SQL)](../t-sql/statements/bulk-insert-transact-sql.md)
