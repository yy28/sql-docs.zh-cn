---
title: 使用 T-SQL （创建外部库） 在 SQL Server 计算机学习 Services 上安装 R 包 |Microsoft 文档
description: 将新的 R 程序包添加到 SQL Server 自 2017 年 1 机器学习 Services （数据库）
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/30/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 7a5a0c394e9a26244661a4ae712d20583c1f1c99
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34585479"
---
# <a name="use-t-sql-create-external-library-to-install-r-packages-on-sql-server-2017-machine-learning-services"></a>使用 T-SQL （创建外部库） 在 SQL Server 自 2017 年 1 机器学习服务上安装 R 包
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

此文章介绍了如何在何处启用机器学习的 SQL Server 实例上安装新的 R 包。 有多个方法可供选择。 使用 T-SQL 的最适合服务器管理员不熟悉。

**适用于：**  [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

[创建外部库](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)语句使可以向特定数据库或实例中添加一个包或一组的包，而无需运行 R 或 Python 代码直接。 但是，此方法需要包准备和附加的数据库权限。

+ 所有包必须都是可用作本地 zip 文件，而不是按需从 internet 下载。

+ 必须由名称和版本，并将 zip 文件中包括所有依赖项。 如果所需包不可用，包括下游包的依赖项，则语句将失败。 

+ 你必须是**db_owner**或在数据库角色中具有创建外部库权限。 有关详细信息，请参阅[创建外部库](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)。

## <a name="download-packages-in-archive-format"></a>下载存档格式中的包

如果你正在安装单个包，下载 zip 格式中的包。

它是更常见的是安装由于包的依赖项的多个包。 当包需要其他包时，必须验证所有这些都彼此在安装期间可访问。 我们建议[创建本地存储库](create-a-local-package-repository-using-minicran.md)使用[miniCRAN](http://andrie.github.io/miniCRAN/)汇集包的完整集合，以及[igraph](http://igraph.org/r/)用于分析包依赖关系。 安装了错误版本的包或省略的包依赖关系可能会导致创建外部库，语句失败。 

## <a name="copy-the-file-to-a-local-folder"></a>将文件复制到本地文件夹

包含所有程序包添加到服务器上的本地文件夹的压缩的文件复制。 如果在服务器上没有对文件系统的访问，你还可以传递一个完整的软件包作为变量，使用的二进制格式。 有关详细信息，请参阅[创建外部库](../../t-sql/statements/create-external-library-transact-sql.md)。

## <a name="run-the-statement-to-upload-packages"></a>运行语句以上载包

打开**查询**窗口中，使用具有管理权限的帐户。

运行 T-SQL 语句`CREATE EXTERNAL LIBRARY`将压缩的包集合上传到数据库。

例如，以下语句名称作为包源 miniCRAN 存储库包含**randomForest**包，以及其依赖项。 

```SQL
CREATE EXTERNAL LIBRARY randomForest
FROM (CONTENT = 'C:\Temp\Rpackages\randomForest_4.6-12.zip')
WITH (LANGUAGE = 'R');
```

不能使用的任意名称;外部库名称必须有期望加载或调用包时要使用的相同名称。

## <a name="verify-package-installation"></a>验证包安装

如果已成功创建了库，你可以通过调用存储过程内 SQL Server 中运行包。
    
```SQL
EXEC sp_execute_external_script
@language =N'R',
@script=N'library(randomForest)'
```

## <a name="see-also"></a>另请参阅

+ [获取包信息](determine-which-packages-are-installed-on-sql-server.md)
+ [R 教程](../tutorials/sql-server-r-tutorials.md)
+ [操作指南](sql-server-machine-learning-tasks.md)