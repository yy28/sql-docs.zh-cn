---
title: 使用 T-SQL （创建外部库） 来安装 R 包的 SQL Server 机器学习服务
description: 将新的 R 包添加到 SQL Server 2016 R Services 或 SQL Server 2017 机器学习服务 （数据库内）。
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/30/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 6e910f1c3b29522b11f1faa83db890d399bf3680
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645046"
---
# <a name="use-t-sql-create-external-library-to-install-r-packages-on-sql-server"></a>使用 T-SQL （创建外部库） 在 SQL Server 上安装 R 包
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文介绍如何在其中启用机器学习的 SQL Server 实例上安装新的 R 包。 有多种方法可供选择。 使用 T-SQL 最适合服务器管理员不熟悉。

**适用于：**  [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

[CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)语句使它可以向特定数据库或实例中添加的包或组的包，而无需运行 R 或 Python 代码直接。 但是，此方法要求包准备和附加数据库的权限。

+ 所有包必须都是可用作本地 zip 文件，而不是按需从 internet 下载。

+ 必须由名称和版本、 标识和 zip 文件中包括所有依赖项。 如果所需的包不可用，包括下游包依赖项，该语句将失败。 

+ 您必须是**db_owner**或数据库角色中具有 CREATE EXTERNAL LIBRARY 权限。 有关详细信息，请参阅[CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)。

## <a name="download-packages-in-archive-format"></a>下载存档格式中的包

如果你正在安装单个包，下载 zip 格式中的包。

它是更常见的安装包依赖项由于多个包。 当包需要其他包时，必须验证所有这些都在安装过程中相互访问。 我们建议[创建本地存储库](create-a-local-package-repository-using-minicran.md)使用[miniCRAN](https://andrie.github.io/miniCRAN/)来组合一套完整的程序包，以及[igraph](https://igraph.org/r/)用于分析的包依赖项。 安装错误版本的包或省略包依赖项可能会导致失败的 CREATE EXTERNAL LIBRARY 语句。 

## <a name="copy-the-file-to-a-local-folder"></a>将文件复制到本地文件夹

复制包含所有程序包添加到服务器上的本地文件夹的压缩的文件。 如果在服务器上没有对文件系统的访问，您还可以传递整个包作为变量，使用二进制格式。 有关详细信息，请参阅[CREATE EXTERNAL LIBRARY](../../t-sql/statements/create-external-library-transact-sql.md)。

## <a name="run-the-statement-to-upload-packages"></a>运行该语句将上传包

打开**查询**窗口中，使用具有管理权限的帐户。

运行 T-SQL 语句`CREATE EXTERNAL LIBRARY`以将压缩的包集合上传到数据库。

例如，以下语句名称作为包的来源 miniCRAN 存储库包含**randomForest**包，以及其依赖项。 

```sql
CREATE EXTERNAL LIBRARY randomForest
FROM (CONTENT = 'C:\Temp\Rpackages\randomForest_4.6-12.zip')
WITH (LANGUAGE = 'R');
```

不能使用任意名称;外部库名称必须具有预期加载或调用包时要使用的相同名称。

## <a name="verify-package-installation"></a>验证包安装

如果已成功创建库，可以通过调用存储过程内 SQL Server 中运行包。
    
```sql
EXEC sp_execute_external_script
@language =N'R',
@script=N'library(randomForest)'
```

## <a name="see-also"></a>另请参阅

+ [获取包信息](determine-which-packages-are-installed-on-sql-server.md)
+ [R 教程](../tutorials/sql-server-r-tutorials.md)
+ [操作指南](sql-server-machine-learning-tasks.md)