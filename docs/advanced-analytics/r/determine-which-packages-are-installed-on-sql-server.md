---
title: "确定 SQL 服务器上安装哪些 R 包 |Microsoft 文档"
ms.custom: 
ms.date: 01/04/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9a7f7e43-b568-406c-9434-5a2ec64ec5f5
caps.latest.revision: "11"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: e76a42ead115c8ee4fa89599b192d722ecfbb2ee
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="determine-which-r-packages-are-installed-on-sql-server"></a>确定 SQL 服务器上安装哪些 R 包

当安装机器学习在 SQL Server 中与 R 语言选项时，R 包库由实例创建专门供使用。 在服务器上的每个实例都有其自己的包库。 无法在实例之间共享包库。

本文介绍如何确定哪些 R 包安装特定的 SQL Server 实例。

## <a name="generate-r-package-list-using-a-stored-procedure"></a>生成使用存储的过程的 R 包列表

下面的示例使用 R 函数`installed.packages()`中[!INCLUDE[tsql](..\..\includes\tsql-md.md)]存储过程来获取的已安装在当前实例的 R_SERVICES 库的包的矩阵。 为避免分析 DESCRIPTION 文件中的字段，仅返回了名称。

```SQL
EXECUTE sp_execute_external_script
@language=N'R'
,@script = N'str(OutputDataSet);
packagematrix <- installed.packages();
NameOnly <- packagematrix[,1];
OutputDataSet <- as.data.frame(NameOnly);'
, @input_data_1 = N''
WITH RESULT SETS ((PackageName nvarchar(250) ))
```

有关可选信息和 R 包描述字段的默认字段，请参阅[https://cran.r-project.org](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file)。

## <a name="verify-whether-a-package-is-installed-with-an-instance"></a>验证是否使用实例安装包

如果你已安装了包，并想要确保它是对特定的 SQL Server 实例可用，则可以执行以下的存储的过程调用，以将包加载，并且返回仅消息。 本示例查找并加载 RevoScaleR 库中，如果可用。

```sql
EXEC sp_execute_external_script  @language =N'R',
@script=N'library("RevoScaleR")'
GO
```

+ 如果找到包，则返回一条消息:"命令已成功完成。"

+ 如果无法找到或加载包，可能会包含文本时出错:"没有名为 MissingPackageName 程序包"

## <a name="get-a-list-of-installed-packages-using-r"></a>获取使用 R 的安装程序包的列表

可通过多种方式使用 R 工具和 R 函数获取已安装或已加载的包的列表。 很多 R 开发工具都提供对象浏览器，或已安装或已在当前 R 工作区中加载的包的列表。 本部分提供了你可以使用从任何 R 命令行或在 sp 某些短命令\_执行\_外部\_脚本。

+ 从本地 R 实用程序，使用基础 R 函数，如`installed.packages()`中, 附带`utils`包。 若要获取的实例的准确列表，您必须显式指定的库路径或使用与实例库关联的 R 工具。

+ 若要检查特定的计算上下文中的包，可以使用 RevoScaleR 包中的下列函数。 这些函数可帮助您识别在指定的计算上下文中的包：

+ [rxFindPackage](https://msdn.microsoft.com/microsoft-r/scaler/packagehelp/rxfindpackage)

+ [rxInstalledPackages](https://msdn.microsoft.com/microsoft-r/scaler/packagehelp/rxinstalledpackages)

例如，运行下面的 R 代码，以获取指定的 SQL Server 计算上下文中提供的程序包的列表。

```r
sqlServerCompute <- RxInSqlServer(connectionString = "Driver=SQL Server;Server=myServer;Database=TestDB;Uid=myID;Pwd=myPwd;")
sqlPackages <- rxInstalledPackages(computeContext = sqlServerCompute)
sqlPackages
```

## <a name="get-library-location-and-version"></a>获取库位置和版本

下面的示例获取在本地计算上下文中，以及程序包版本 RevoScaleR 的库位置。

```r
rxFindPackage(RevoScaleR, "local")
packageVersion("RevoScaleR")
```

## <a name="determine-path-of-library-used-by-sql-server"></a>确定 SQL Server 使用的库路径

如果你已升级机器学习使用绑定的组件，可能会更改 R 库的路径。 在此情况下，R 工具的以前快捷方式可能引用的早期版本。 若要确保的 SQL Server 使用的路径和包版本，你可以运行如下命令：

```sql
EXEC sp_execute_external_script
    @language =N'R',
    @script=N'
    sql_r_path <- rxSqlLibPaths("local")
      print(sql_r_path)
    version_info <-packageVersion("RevoScaleR")
      print(version_info)'
```

**结果**

```text
STDOUT message(s) from external script: 
[1] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER1000/R_SERVICES/library"
[1] '9.2.1'
```
## <a name="see-also"></a>另请参阅

[在 SQL Server 上安装其他 R 包](install-additional-r-packages-on-sql-server.md)
