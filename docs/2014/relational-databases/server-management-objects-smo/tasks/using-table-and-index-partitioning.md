---
title: 使用表和索引分区 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- partitions [SMO]
- storing data [SMO]
- partitioned tables [SQL Server], SMO
- partitioned indexes [SQL Server], SMO
ms.assetid: 0e682d7e-86c3-4d73-950d-aa692d46cb62
caps.latest.revision: 43
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: db31f674605b1cf1c75351e6241ff6aed2b282c7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37221007"
---
# <a name="using-table-and-index-partitioning"></a>使用表和索引分区
  数据可以存储通过使用提供的存储算法[Partitioned Tables and Indexes](../../partitions/partitioned-tables-and-indexes.md)。 分区可以使大型表和索引更易于管理并且更灵活。  
  
## <a name="index-and-table-partitioning"></a>索引和表分区  
 通过该功能可以将索引和表数据分散到各个分区中的多个文件组。 分区函数定义如何根据某些列（称为分区依据列）中的值将表或索引的行映射到一组分区。 分区方案将分区函数指定的每个分区映射到一个文件组。 这样，您便可以制定相应存档策略，用以将表扩展到多个文件组，因而也可扩展到多个物理设备。  
  
 <xref:Microsoft.SqlServer.Management.Smo.Database>对象包含一系列<xref:Microsoft.SqlServer.Management.Smo.PartitionFunction>对象表示实现的分区函数和一系列<xref:Microsoft.SqlServer.Management.Smo.PartitionScheme>描述如何将数据映射到文件组的对象。  
  
 每个 <xref:Microsoft.SqlServer.Management.Smo.Table> 和 <xref:Microsoft.SqlServer.Management.Smo.Index> 对象在 <xref:Microsoft.SqlServer.Management.Smo.PartitionScheme> 属性中指定其使用的分区方案，并在 <xref:Microsoft.SqlServer.Management.Smo.PartitionSchemeParameterCollection> 中指定列。  
  
## <a name="example"></a>示例  
 对于下面的代码示例，您必须选择编程环境、编程模板和编程语言才能创建应用程序。 有关详细信息，请参阅[在 Visual Studio.NET 中创建 Visual Basic SMO 项目](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md)并[创建 Visual C&#35; Visual Studio.NET 中的 SMO 项目](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。  
  
## <a name="setting-up-a-partition-scheme-for-a-table-in-visual-basic"></a>在 Visual Basic 中为表设置分区方案  
 代码示例演示如何创建分区函数和分区方案为`TransactionHistory`表中[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)]示例数据库。 这些分区是按日期划分的，这样做的目的是将以前的记录分离出来，放入 `TransactionHistoryArchive` 表中。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBPartition1](SMO How to#SMO_VBPartition1)]  -->  
  
## <a name="setting-up-a-partition-scheme-for-a-table-in-visual-c"></a>在 Visual C# 中为表设置分区方案  
 代码示例演示如何创建分区函数和分区方案为`TransactionHistory`表中[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)]示例数据库。 这些分区是按日期划分的，这样做的目的是将以前的记录分离出来，放入 `TransactionHistoryArchive` 表中。  
  
```  
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Reference the AdventureWorks2012 database.   
Database db;   
db = srv.Databases("AdventureWorks2012");   
//Define and create three new file groups on the database.   
FileGroup fg2;   
fg2 = new FileGroup(db, "Second");   
fg2.Create();   
FileGroup fg3;   
fg3 = new FileGroup(db, "Third");   
fg3.Create();   
FileGroup fg4;   
fg4 = new FileGroup(db, "Fourth");   
fg4.Create();   
//Define a partition function by supplying the parent database and name arguments in the constructor.   
PartitionFunction pf;   
pf = new PartitionFunction(db, "TransHistPF");   
//Add a partition function parameter that specifies the function uses a DateTime range type.   
PartitionFunctionParameter pfp;   
pfp = new PartitionFunctionParameter(pf, DataType.DateTime);   
pf.PartitionFunctionParameters.Add(pfp);   
//Specify the three dates that divide the data into four partitions.   
object[] val;   
val = new object[] {"1/1/2003", "1/1/2004", "1/1/2005"};   
pf.RangeValues = val;   
//Create the partition function.   
pf.Create();   
//Define a partition scheme by supplying the parent database and name arguments in the constructor.   
PartitionScheme ps;   
ps = new PartitionScheme(db, "TransHistPS");   
//Specify the partition function and the filegroups required by the partition scheme.   
ps.PartitionFunction = "TransHistPF";   
ps.FileGroups.Add("PRIMARY");   
ps.FileGroups.Add("second");   
ps.FileGroups.Add("Third");   
ps.FileGroups.Add("Fourth");   
//Create the partition scheme.   
ps.Create();   
}   
```  
  
## <a name="setting-up-a-partition-scheme-for-a-table-in-powershell"></a>在 PowerShell 中为表设置分区方案  
 代码示例演示如何创建分区函数和分区方案为`TransactionHistory`表中[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)]示例数据库。 这些分区是按日期划分的，这样做的目的是将以前的记录分离出来，放入 `TransactionHistoryArchive` 表中。  
  
```powershell  
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\default  
  
#Get a server object which corresponds to the default instance  
$srv = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
$db = $srv.Databases["AdventureWorks"]  
#Create four filegroups  
$fg1 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Filegroup -argumentlist $db, "First"  
$fg2 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Filegroup -argumentlist $db, "Second"  
$fg3 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Filegroup -argumentlist $db, "Third"  
$fg4 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Filegroup -argumentlist $db, "Fourth"  
  
#Define a partition function by supplying the parent database and name arguments in the constructor.  
$pf =  New-Object -TypeName Microsoft.SqlServer.Management.SMO.PartitionFunction -argumentlist $db, "TransHistPF"  
$T = [Microsoft.SqlServer.Management.SMO.DataType]::DateTime  
$T  
$T.GetType()  
#Add a partition function parameter that specifies the function uses a DateTime range type.  
$pfp =  New-Object -TypeName Microsoft.SqlServer.Management.SMO.PartitionFunctionParameter -argumentlist $pf, $T  
  
#Specify the three dates that divide the data into four partitions.   
#Create an array of type object to hold the partition data  
$val = "1/1/2003"."1/1/2004","1/1/2005"  
$pf.RangeValues = $val  
$pf  
#Create the partition function  
$pf.Create()  
  
#Create partition scheme  
$ps = New-Object -TypeName Microsoft.SqlServer.Management.SMO.PartitionScheme -argumentlist $db, "TransHistPS"  
$ps.PartitionFunction = "TransHistPF"  
  
#add the filegroups to the scheme   
$ps.FileGroups.Add("PRIMARY")  
$ps.FileGroups.Add("Second")  
$ps.FileGroups.Add("Third")  
$ps.FileGroups.Add("Fourth")  
  
#Create it at the server  
$ps.Create()  
```  
  
## <a name="see-also"></a>请参阅  
 [Partitioned Tables and Indexes](../../partitions/partitioned-tables-and-indexes.md)  
  
  
