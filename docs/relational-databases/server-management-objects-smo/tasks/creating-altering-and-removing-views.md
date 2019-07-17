---
title: 创建、 更改和删除视图 |Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- views [SMO]
ms.assetid: 7d445c0e-77ef-4734-993b-e022de31df23
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f2851cab846e8f814e03e2b96ad10c69136c9a27
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68111496"
---
# <a name="creating-altering-and-removing-views"></a>创建、更改和删除视图
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]
  在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 管理对象 (SMO) 中，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 视图由 <xref:Microsoft.SqlServer.Management.Smo.View> 对象表示。  
  
 <xref:Microsoft.SqlServer.Management.Smo.View.TextBody%2A> 对象的 <xref:Microsoft.SqlServer.Management.Smo.View> 属性可定义视图。 它与创建视图的 [!INCLUDE[tsql](../../../includes/tsql-md.md)] SELECT 语句等效。  
  
## <a name="example"></a>示例  
 若要使用所提供的任何代码示例，您必须选择创建应用程序所需的编程环境、编程模板和编程语言。 有关详细信息，请参阅[创建 Visual C&#35; Visual Studio.NET 中的 SMO 项目](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。  
  
## <a name="creating-altering-and-removing-a-view-in-visual-basic"></a>在 Visual Basic 中创建、更改和删除视图  
 此代码示例显示如何使用内部联接创建两个表的视图。 该视图是使用文本模式创建的，因此必须设置 <xref:Microsoft.SqlServer.Management.Smo.View.TextHeader%2A> 属性。  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Reference the AdventureWorks2012 2008R2 database.
Dim db As Database
db = srv.Databases("AdventureWorks2012")
'Define a View object variable by supplying the parent database, view name and schema in the constructor.
Dim myview As View
myview = New View(db, "Test_View", "Sales")
'Set the TextHeader and TextBody property to define the view.
myview.TextHeader = "CREATE VIEW [Sales].[Test_View] AS"
myview.TextBody = "SELECT h.SalesOrderID, d.OrderQty FROM Sales.SalesOrderHeader AS h INNER JOIN Sales.SalesOrderDetail AS d ON h.SalesOrderID = d.SalesOrderID"
'Create the view on the instance of SQL Server.
myview.Create()
'Remove the view.
myview.Drop()
```
  
## <a name="creating-altering-and-removing-a-view-in-visual-c"></a>在 Visual C# 中创建、更改和删除视图  
 此代码示例显示如何使用内部联接创建两个表的视图。 该视图是使用文本模式创建的，因此必须设置 <xref:Microsoft.SqlServer.Management.Smo.View.TextHeader%2A> 属性。  
  
```csharp  
{  
        //Connect to the local, default instance of SQL Server.   
        Server srv;   
        srv = new Server();   
        //Reference the AdventureWorks2012 database.   
        Database db;   
        db = srv.Databases["AdventureWorks2012"];   
        //Define a View object variable by supplying the parent database, view name and schema in the constructor.   
        View myview;   
        myview = new View(db, "Test_View", "Sales");   
        //Set the TextHeader and TextBody property to define the view.   
        myview.TextHeader = "CREATE VIEW [Sales].[Test_View] AS";   
        myview.TextBody = "SELECT h.SalesOrderID, d.OrderQty FROM Sales.SalesOrderHeader AS h INNER JOIN Sales.SalesOrderDetail AS d ON h.SalesOrderID = d.SalesOrderID";   
        //Create the view on the instance of SQL Server.   
        myview.Create();   
        //Remove the view.   
        myview.Drop();   
        }  
```  
  
## <a name="creating-altering-and-removing-a-view-in-powershell"></a>在 PowerShell 中创建、更改和删除视图  
 此代码示例显示如何使用内部联接创建两个表的视图。 该视图是使用文本模式创建的，因此必须设置 <xref:Microsoft.SqlServer.Management.Smo.View.TextHeader%2A> 属性。  
  
```powershell   
# Set the path context to the local, default instance of SQL Server and get a reference to AdventureWorks2012  
CD \sql\localhost\default\databases  
$db = get-item Adventureworks2012  
  
# Define a View object variable by supplying the parent database, view name and schema in the constructor.   
$myview  = New-Object -TypeName Microsoft.SqlServer.Management.SMO.View `  
-argumentlist $db, "Test_View", "Sales"  
  
# Set the TextHeader and TextBody property to define the view.   
$myview.TextHeader = "CREATE VIEW [Sales].[Test_View] AS"  
$myview.TextBody ="SELECT h.SalesOrderID, d.OrderQty FROM Sales.SalesOrderHeader AS h INNER JOIN Sales.SalesOrderDetail AS d ON h.SalesOrderID = d.SalesOrderID"  
  
# Create the view on the instance of SQL Server.   
$myview.Create()  
  
# Remove the view.   
$myview.Drop();  
```  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.SqlServer.Management.Smo.View>  
  
  
