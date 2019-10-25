---
title: 创建、更改和删除数据库 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- databases [SMO]
- databases [SMO], creating
- databases [SMO], modifying
- databases [SMO], deleting
ms.assetid: fcfb3ec2-7556-4f72-971a-501295892cb0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 645ba8428dddb36de9a3edeb784d64f96b5c0603
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/23/2019
ms.locfileid: "72797036"
---
# <a name="creating-altering-and-removing-databases"></a>创建、更改和删除数据库
  在 SMO 中，数据库由 <xref:Microsoft.SqlServer.Management.Smo.Database> 对象表示。  
  
 不必创建 <xref:Microsoft.SqlServer.Management.Smo.Database> 对象便可修改或删除数据库。 通过使用集合可以引用数据库。  
  
## <a name="example"></a>示例  
 若要使用所提供的任何代码示例，您必须选择创建应用程序所需的编程环境、编程模板和编程语言。 有关详细信息，请参阅[在 Visual studio .net 中创建 VISUAL BASIC SMO 项目](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md)或[在 visual Studio&#35; .Net 中创建 visual C SMO 项目](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。  
  
## <a name="creating-altering-and-removing-a-database-in-visual-basic"></a>在 Visual Basic 中创建、更改和删除数据库  
 此代码示例创建了一个新数据库。 将为该数据库自动创建文件和文件组。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBDatabase1](SMO How to#SMO_VBDatabase1)]  -->  
  
## <a name="creating-altering-and-removing-a-database-in-visual-c"></a>在 Visual C# 中创建、更改和删除数据库  
 此代码示例创建了一个新数据库。 将为该数据库自动创建文件和文件组。  
  
```csharp
{  
                //Connect to the local, default instance of SQL Server.   
                Server srv;  
                srv = new Server();  
                //Define a Database object variable by supplying the server and the database name arguments in the constructor.   
                Database db;  
                db = new Database(srv, "Test_SMO_Database");  
                //Create the database on the instance of SQL Server.   
                db.Create();  
                //Reference the database and display the date when it was created.   
                db = srv.Databases["Test_SMO_Database"];  
                Console.WriteLine(db.CreateDate);  
                //Remove the database.   
                db.Drop();  
            }  
```  
  
## <a name="creating-altering-and-removing-a-database-in-powershell"></a>在 PowerShell 中创建、更改和删除数据库  
 此代码示例创建了一个新数据库。 将为该数据库自动创建文件和文件组。  
  
```powershell
#Get a server object which corresponds to the default instance  
cd \sql\localhost\  
$srv = Get-Item default  
  
#Create a new database  
$db = New-Object -TypeName Microsoft.SqlServer.Management.Smo.Database -argumentlist $srv, "Test_SMO_Database"  
$db.Create()  
  
#Reference the database and display the date when it was created.
$db = $srv.Databases["Test_SMO_Database"]  
$db.CreateDate  
  
#Drop the database  
$db.Drop()  
```  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.SqlServer.Management.Smo.Database>  
