---
title: "确定要在 SQL Server 上安装的包 | Microsoft Docs"
ms.custom: ""
ms.date: "08/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9a7f7e43-b568-406c-9434-5a2ec64ec5f5
caps.latest.revision: 11
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 10
---
# 确定要在 SQL Server 上安装的包
  本主题介绍如何确定哪些 R 包安装在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。  
  
默认情况下，安装 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 创建与每个实例相关联的 R 包库。 因此，若要了解哪些包安装在一台计算机上，您必须在安装了 R Services 每个单独实例上运行此查询。 请注意，包库 **不** 在实例之间共享，因此很可能不同的包安装在不同实例上。

有关如何确定实例的默认库位置的信息，请参阅 [安装和管理多个 R 包](../../advanced-analytics/r-services/installing-and-managing-r-packages.md)。   
   
 
## 获取使用 R 的已安装程序包的列表  
 有多种方法来获取已安装或已加载的包使用 R 的工具和 R 函数的列表。  
  
+   很多 R 开发工具都提供对象浏览器，或已安装或已在当前 R 工作区中加载的包的列表。  

+ 我们建议专门为将管理包中提供的以下函数从 RevoScaleR 包计算上下文︰
  - [rxFindPackage](https://msdn.microsoft.com/microsoft-r/scaler/rxfindpackage)
  - [rxInstalledPackages](https://msdn.microsoft.com/microsoft-r/scaler/rxInstalledPackages)   
  
+   你可以使用已安装的 `installed.packages()`包中的 R 函数，如 `utils` 。 该函数会扫描每个包，它指定在库中找到并返回的包名称、 库路径和版本号的矩阵的说明文件。  
 
### 示例  
下面的示例使用函数 `rxInstalledPackages` 来获取所提供的 SQL Server 计算上下文中提供的程序包列表。

~~~~
sqlServerCompute <- RxInSqlServer(connectionString = 
"Driver=SQL Server;Server=myServer;Database=TestDB;Uid=myID;Pwd=myPwd;")
     sqlPackages <- rxInstalledPackages(computeContext = sqlServerCompute)
     sqlPackages
~~~~

 下面的示例使用基础 R 函数 `installed.packages()` 中 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存储过程来获得已安装在当前实例的 R_SERVICES 库的程序包的矩阵。 为避免分析 DESCRIPTION 文件中的字段，仅返回了名称。  
  
```  
EXECUTE sp_execute_external_script  
@language=N'R'  
,@script = N'str(OutputDataSet);  
packagematrix <- installed.packages();  
NameOnly <- packagematrix[,1];  
OutputDataSet <- as.data.frame(NameOnly);'  
,@input_data_1 = N'SELECT 1 as col'  
WITH RESULT SETS ((PackageName nvarchar(250) ))  
```  
  
 有关默认和可选字段在 R 包说明文件的详细信息，请参阅 [https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file](https://cran.r-project.org/doc/manuals/R-exts.html)。  
  
## 另请参阅  
 [在 SQL Server 上安装其他 R 包](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md)  
  
  