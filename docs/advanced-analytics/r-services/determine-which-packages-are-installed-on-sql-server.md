---
title: "确定要在 SQL Server 上安装的包 | Microsoft Docs"
ms.custom: 
ms.date: 08/31/2016
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
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: e14d47ff3b545d64436cbe195c31348ee000c6c7
ms.lasthandoff: 04/11/2017

---
# <a name="determine-which-packages-are-installed-on-sql-server"></a>确定要在 SQL Server 上安装的包
  本主题介绍如何确定要在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上安装的 R 包。  
  
默认情况下，安装 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 会创建与每个实例关联的 R 包库。 因此，若要了解哪些包将安装在计算机上，必须在安装了 R Services 的每个单独实例上运行此查询。 请注意，包库**不**会在实例之间共享，因此很可能不同的包安装在不同实例上。

有关如何确定实例的默认库位置的信息，请参阅[安装和管理 R 包](../../advanced-analytics/r-services/installing-and-managing-r-packages.md)。   
   
 
## <a name="get-a-list-of-installed-packages-using-r"></a>使用 R 获取已安装的包列表  
 可通过多种方式使用 R 工具和 R 函数获取已安装或已加载的包的列表。  
  
+   很多 R 开发工具都提供对象浏览器，或已安装或已在当前 R 工作区中加载的包的列表。  

+ 我们建议使用 RevoScaleR 包中的以下函数，这些函数专用于在计算上下文中管理包：
  - [rxFindPackage](https://msdn.microsoft.com/microsoft-r/scaler/rxfindpackage)
  - [rxInstalledPackages](https://msdn.microsoft.com/microsoft-r/scaler/rxInstalledPackages)   
  
+   你可以使用已安装的 `installed.packages()`包中的 R 函数，如 `utils` 。 该函数会扫描在指定库中找到的每个包的 DESCRIPTION 文件，并返回包名称、库路径和版本号的矩阵。  
 
### <a name="examples"></a>示例  
以下示例使用函数 `rxInstalledPackages` 获取在所提供的 SQL Server 计算上下文中可用的包的列表。

~~~~
sqlServerCompute <- RxInSqlServer(connectionString = 
"Driver=SQL Server;Server=myServer;Database=TestDB;Uid=myID;Pwd=myPwd;")
     sqlPackages <- rxInstalledPackages(computeContext = sqlServerCompute)
     sqlPackages
~~~~

 以下示例在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 存储过程中使用基础 R 函数 `installed.packages()` 来获取已安装在当前实例的 R_SERVICES 库中的包的矩阵。 为避免分析 DESCRIPTION 文件中的字段，仅返回了名称。  
  
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
  
 有关详细信息，请在以下网址参阅 R 包 DESCRIPTION 文件的可选和默认字段的说明：[https://cran.r-project.org](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file)。  
  
## <a name="see-also"></a>另请参阅  
 [在 SQL Server 上安装其他 R 包](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md)  
  
  

