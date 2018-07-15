---
title: 使用文件组和存储数据文件 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- filegroups [SMO]
- storing data [SMO]
- files [SMO]
- files [SMO], about files
- storage [SMO]
ms.assetid: 7e2327ce-e1a6-4904-83d1-0944b24a7b43
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bd05be78281375f75cca679b3cdbfcb269a984c2
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37324367"
---
# <a name="using-filegroups-and-files-to-store-data"></a>使用文件组和文件存储数据
  数据文件可用于存储数据库文件。 数据文件可细分为文件组。 <xref:Microsoft.SqlServer.Management.Smo.Database> 对象具有 <xref:Microsoft.SqlServer.Management.Smo.Database.FileGroups%2A> 属性，该属性引用 <xref:Microsoft.SqlServer.Management.Smo.FileGroupCollection> 对象。 该集合中的每个 <xref:Microsoft.SqlServer.Management.Smo.FileGroup> 对象都具有 <xref:Microsoft.SqlServer.Management.Smo.FileGroup.Files%2A> 属性。 此属性引用 <xref:Microsoft.SqlServer.Management.Smo.DataFileCollection> 集合，该集合包含属于数据库的所有数据文件。 文件组主要用于将用于存储数据库对象的文件组合在起来。 将一个数据库对象分布到几个文件上的一个原因是，它可以提高性能，尤其是在文件存储在不同磁盘驱动器上时。  
  
 自动创建的每个数据库都具有一个名为“Primary”的文件组和一个与数据库同名的数据文件。 其他文件和组可以添加到集合中。  
  
## <a name="examples"></a>示例  
 对于下列代码示例，您必须选择编程环境、编程模板和编程语言才能创建应用程序。 有关详细信息，请参阅[在 Visual Studio.NET 中创建 Visual Basic SMO 项目](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md)并[创建 Visual C&#35; Visual Studio.NET 中的 SMO 项目](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。  
  
## <a name="adding-filegroups-and-datafiles-to-a-database-in-visual-basic"></a>在 Visual Basic 中将 FileGroups 和 DataFiles 添加到数据库  
 主文件组和数据文件将自动使用默认属性值创建。 代码示例指定了一些可以使用的属性值。 否则，将使用默认属性值。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBFileGroups1](SMO How to#SMO_VBFileGroups1)]  -->  
  
## <a name="adding-filegroups-and-datafiles-to-a-database-in-visual-c"></a>在 Visual C# 中将 FileGroups 和 DataFiles 添加到数据库  
 主文件组和数据文件将自动使用默认属性值创建。 代码示例指定了一些可以使用的属性值。 否则，将使用默认属性值。  
  
```  
{  
            Server srv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database db = default(Database);  
            db = srv.Databases["AdventureWorks2012"];  
            //Define a FileGroup object called SECONDARY on the database.   
            FileGroup fg1 = default(FileGroup);  
            fg1 = new FileGroup(db, "SECONDARY");  
            //Call the Create method to create the file group on the instance of SQL Server.   
            fg1.Create();  
            //Define a DataFile object on the file group and set the FileName property.   
            DataFile df1 = default(DataFile);  
            df1 = new DataFile(fg1, "datafile1");  
            df1.FileName = "c:\\Program Files\\Microsoft SQL Server\\MSSQL.1\\MSSQL\\Data\\datafile2.ndf";  
            //Call the Create method to create the data file on the instance of SQL Server.   
            df1.Create();  
        }  
```  
  
## <a name="adding-filegroups-and-datafiles-to-a-database-in-powershell"></a>在 PowerShell 中将 FileGroups 和 DataFiles 添加到数据库  
 主文件组和数据文件将自动使用默认属性值创建。 代码示例指定了一些可以使用的属性值。 否则，将使用默认属性值。  
  
```  
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\default\Databases\  
  
#And the database object corresponding to AdventureWorks2012.  
$db = get-item AdventureWorks2012  
  
#Create a new filegroup  
$fg1 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Filegroup -argumentlist $db, "SECONDARY"  
$fg1.Create()  
  
#Define a DataFile object on the file group and set the FileName property.   
$df1 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.DataFile -argumentlist $fg1, "datafile1"  
  
#Make sure to have a directory created to hold the designated data file  
$df1.FileName = "c:\\TestData\\datafile2.ndf"  
  
#Call the Create method to create the data file on the instance of SQL Server.   
$df1.Create()  
```  
  
## <a name="creating-altering-and-removing-a-log-file-in-visual-basic"></a>在 Visual Basic 中创建、更改和删除日志文件  
 代码示例将创建 <xref:Microsoft.SqlServer.Management.Smo.LogFile> 对象，更改其中一个属性，然后将其从数据库中删除。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBFileGroups3](SMO How to#SMO_VBFileGroups3)]  -->  
  
## <a name="creating-altering-and-removing-a-log-file-in-visual-c"></a>在 Visual C# 中创建、更改和删除日志文件  
 代码示例将创建 <xref:Microsoft.SqlServer.Management.Smo.LogFile> 对象，更改其中一个属性，然后将其从数据库中删除。  
  
```  
//Connect to the local, default instance of SQL Server.   
            Server srv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database db = default(Database);  
            db = srv.Databases["AdventureWorks2012"];  
            //Define a LogFile object and set the database, name, and file name properties in the constructor.   
            LogFile lf1 = default(LogFile);  
            lf1 = new LogFile(db, "logfile1", "c:\\Program Files\\Microsoft SQL Server\\MSSQL.10_50.MSSQLSERVER\\MSSQL\\Data\\logfile1.ldf");  
            //Set the file growth to 6%.   
            lf1.GrowthType = FileGrowthType.Percent;  
            lf1.Growth = 6;  
            //Run the Create method to create the log file on the instance of SQL Server.   
            lf1.Create();  
            //Alter the growth percentage.   
            lf1.Growth = 7;  
            lf1.Alter();  
            //Remove the log file.   
            lf1.Drop();  
  
```  
  
## <a name="creating-altering-and-removing-a-log-file-in-powershell"></a>在 PowerShell 中创建、更改和删除日志文件  
 代码示例将创建 <xref:Microsoft.SqlServer.Management.Smo.LogFile> 对象，更改其中一个属性，然后将其从数据库中删除。  
  
```  
#Load the assembly containing the enums used in this example  
[reflection.assembly]::LoadWithPartialName("Microsoft.SqlServer.SqlEnum")  
  
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\default\Databases\  
  
#And the database object corresponding to AdventureWorks2012  
$db = get-item AdventureWorks2012  
  
#Create a filegroup  
$fg1 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Filegroup -argumentlist $db, "Secondary"  
  
#Call the Create method to create the file group on the instance of SQL Server.   
$fg1.Create()  
  
#Define a LogFile object on the file group and set the FileName property.   
$lf1 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.LogFile -argumentlist $db, "LogFile2"  
  
#Set a location for it - make sure the directory exists  
$lf1.FileName = "logfile1", "c:\\Program Files\\Microsoft SQL Server\\MSSQL.10_50.MSSQLSERVER\\MSSQL\\Data\\logfile1.ldf"  
  
#Set file growth to 6%  
$lf1.GrowthType = [Microsoft.SqlServer.Management.Smo.FileGrowthType]::Percent  
$lf1.Growth = 6.0  
  
#Call the Create method to create the data file on the instance of SQL Server.   
$lf1.Create()  
  
#Alter a value and drop the log file  
$lf1.Growth = 7.0  
$lf1.Alter()  
$lf1.Drop()  
  
```  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.SqlServer.Management.Smo.FileGroup>   
 [数据库文件和文件组](../../databases/database-files-and-filegroups.md)  
  
  
