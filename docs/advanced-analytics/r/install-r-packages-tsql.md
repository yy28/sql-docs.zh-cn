---
title: 使用 T-sql (创建外部库) 安装 R 包
description: 将新的 R 包添加到 SQL Server 2016 R Services 或 SQL Server 机器学习服务 (数据库内)。
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/12/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 1acaae39d71abd1cbd68781c0edec76308b85760
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715732"
---
# <a name="use-t-sql-create-external-library-to-install-r-packages-on-sql-server"></a>使用 T-sql (创建外部库) 在 SQL Server 上安装 R 包
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文介绍如何在启用机器学习的 SQL Server 实例上安装新的 R 包。 有多种方法可供选择。 使用 T-sql 最适用于不熟悉 R 的服务器管理员。

**适用于:** [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)]  [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

[CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)语句使你可以将包或包集添加到实例或特定数据库, 而无需直接运行 R 或 Python 代码。 但是, 此方法需要包准备和额外的数据库权限。

+ 所有包都必须作为本地压缩文件提供, 而不是从 internet 按需下载。

+ 必须按名称和版本标识所有依赖项, 并将其包含在 zip 文件中。 如果所需的包不可用, 则语句将失败, 包括下游包依赖项。 

+ 您必须是**db_owner**或具有数据库角色中的 CREATE EXTERNAL LIBRARY 权限。 有关详细信息, 请参阅[创建外部库](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)。

## <a name="download-packages-in-archive-format"></a>下载存档格式的包

如果要安装单个包, 请下载压缩格式的包。

由于包的依赖关系, 因此更常见的方法是安装多个包。 当包需要其他包时, 必须在安装过程中验证是否所有包都可以访问。 建议使用[miniCRAN](https://andrie.github.io/miniCRAN/) [创建本地存储库](create-a-local-package-repository-using-minicran.md), 以组合包的完整集合, 以及用于分析包依赖项的[igraph](https://igraph.org/r/) 。 安装包的错误版本或省略包依赖项可能导致 CREATE EXTERNAL LIBRARY 语句失败。 

## <a name="copy-the-file-to-a-local-folder"></a>将文件复制到本地文件夹

将包含所有包的压缩文件复制到服务器上的本地文件夹。 如果您无法访问服务器上的文件系统, 还可以使用二进制格式将整个包作为变量传递。 有关详细信息, 请参阅[CREATE EXTERNAL LIBRARY](../../t-sql/statements/create-external-library-transact-sql.md)。

## <a name="run-the-statement-to-upload-packages"></a>运行语句上传包

使用具有管理权限的帐户打开**查询**窗口。

运行 t-sql 语句`CREATE EXTERNAL LIBRARY` , 将压缩包集合上传到数据库。

例如, 以下语句名称为包源, 其中包含**randomForest**包及其依赖项的 miniCRAN 存储库。 

```sql
CREATE EXTERNAL LIBRARY randomForest
FROM (CONTENT = 'C:\Temp\Rpackages\randomForest_4.6-12.zip')
WITH (LANGUAGE = 'R');
```

不能使用任意名称;外部库名称的名称必须与加载或调用包时预期使用的名称相同。

## <a name="verify-package-installation"></a>验证包安装

如果库已成功创建, 则可以在 SQL Server 中运行包, 方法是在存储过程中调用包。
    
```sql
EXEC sp_execute_external_script
@language =N'R',
@script=N'library(randomForest)'
```

## <a name="see-also"></a>请参阅

+ [获取包信息](../package-management/installed-package-information.md)
+ [R 教程](../tutorials/sql-server-r-tutorials.md)
