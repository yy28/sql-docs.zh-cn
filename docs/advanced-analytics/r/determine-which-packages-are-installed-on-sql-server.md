---
title: "确定 SQL 服务器上安装哪些 R 包 |Microsoft 文档"
ms.custom: 
ms.date: 10/09/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9a7f7e43-b568-406c-9434-5a2ec64ec5f5
caps.latest.revision: 11
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 29122bdf543e82c1f429cf401b5fe1d8383515fc
ms.openlocfilehash: 138368a3ca212cb4c176df57d78d02b6f41c4344
ms.contentlocale: zh-cn
ms.lasthandoff: 10/10/2017

---
# <a name="determine-which-r-packages-are-installed-on-sql-server"></a>确定 SQL 服务器上安装哪些 R 包

当安装机器学习在 SQL Server 中与 R 语言选项时，安装程序将创建与实例关联的 R 包库。 每个实例都有单独的包库。 包库**不**实例之间共享，因此可能会在不同的包安装在不同的实例上。

本文介绍如何确定哪些 R 包安装特定实例。

## <a name="generate-r-package-list-using-a-stored-procedure"></a>生成使用存储的过程的 R 包列表

下面的示例使用 R 函数`installed.packages()`中[!INCLUDE[tsql](..\..\includes\tsql-md.md)]存储过程来获取的已安装在当前实例的 R_SERVICES 库的包的矩阵。 为避免分析 DESCRIPTION 文件中的字段，仅返回了名称。

```SQL
EXECUTE sp_execute_external_script
@language=N'R'  
,@script = N'str(OutputDataSet);  
packagematrix <- installed.packages();  
NameOnly <- packagematrix[,1];  
OutputDataSet <- as.data.frame(NameOnly);'  
,@input_data_1 = N'SELECT 1 as col'  
WITH RESULT SETS ((PackageName nvarchar(250) ))  
```

有关可选信息和 R 包说明文件的默认字段，请参阅[https://cran.r-project.org](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file)。

## <a name="verify-whether-a-package-is-installed-with-an-instance"></a>验证是否使用实例安装包

如果你已安装了包，并想要确保它是对特定的 SQL Server 实例可用，则可以执行以下的存储的过程调用，以将包加载，并且返回仅消息。

```SQL
EXEC sp_execute_external_script  @language =N'R',
@script=N'library("RevoScaleR")'
GO
```

本示例查找并加载 RevoScaleR 库。

+ 如果找到包，则返回的消息应类似"命令已成功完成。"

+ 如果无法找到或加载包，你收到如下错误:"外部脚本出错： library("RevoScaleR") 时出错： 没有调用 RevoScaleR 程序包"

## <a name="get-a-list-of-installed-packages-using-r"></a>获取使用 R 的安装程序包的列表

可通过多种方式使用 R 工具和 R 函数获取已安装或已加载的包的列表。 很多 R 开发工具都提供对象浏览器，或已安装或已在当前 R 工作区中加载的包的列表。

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
## <a name="see-also"></a>另请参阅

[在 SQL Server 上安装其他 R 包](install-additional-r-packages-on-sql-server.md)

