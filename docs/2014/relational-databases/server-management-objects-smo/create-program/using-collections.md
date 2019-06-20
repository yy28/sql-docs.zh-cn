---
title: 使用集合 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQL Server Management Objects, collections
- SMO [SQL Server], collections
- collections [SMO]
ms.assetid: 209eb175-2514-4de1-bc32-b2e6a469d945
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0be31e67be0b80de13a9239b221ca73436a8d6e7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63192123"
---
# <a name="using-collections"></a>使用集合
  集合是指从相同对象类构造的并共享同一父对象的对象列表。 集合对象始终包含对象类型的名称并具有 Collection 后缀。 例如，若要访问指定表中的列，请使用 <xref:Microsoft.SqlServer.Management.Smo.ColumnCollection> 对象类型。 它包含所有属于同一 <xref:Microsoft.SqlServer.Management.Smo.Column> 对象的 <xref:Microsoft.SqlServer.Management.Smo.Table> 对象。  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] `For...Each`语句或[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[csprcs](../../../includes/csprcs-md.md)] `foreach`语句可用于循环访问集合中的每个成员。  
  
## <a name="examples"></a>示例  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="referencing-an-object-by-using-a-collection-in-visual-basic"></a>在 Visual Basic 中使用集合来引用对象  
 此代码示例演示如何使用 <xref:Microsoft.SqlServer.Management.Smo.TableViewTableTypeBase.Columns%2A>、<xref:Microsoft.SqlServer.Management.Smo.Database.Tables%2A> 和 <xref:Microsoft.SqlServer.Management.Smo.Server.Databases%2A> 属性来设置列属性。 这些属性表示集合，当这些属性与指定对象名称的参数一起使用时可用来标识特定对象。 <xref:Microsoft.SqlServer.Management.Smo.Database.Tables%2A> 集合对象属性需要名称和架构。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBCollections1](SMO How to#SMO_VBCollections1)]  -->  
  
## <a name="referencing-an-object-by-using-a-collection-in-visual-c"></a>在 Visual C# 中使用集合来引用对象  
 此代码示例演示如何使用 <xref:Microsoft.SqlServer.Management.Smo.TableViewTableTypeBase.Columns%2A>、<xref:Microsoft.SqlServer.Management.Smo.Database.Tables%2A> 和 <xref:Microsoft.SqlServer.Management.Smo.Server.Databases%2A> 属性来设置列属性。 这些属性表示集合，当这些属性与指定对象名称的参数一起使用时可用来标识特定对象。 <xref:Microsoft.SqlServer.Management.Smo.Database.Tables%2A> 集合对象属性需要名称和架构。  
  
```  
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Modify a property using the Databases, Tables, and Columns collections to reference a column.   
srv.Databases("AdventureWorks2012").Tables("Person", "Person").Columns("LastName").Nullable = true;   
//Call the Alter method to make the change on the instance of SQL Server.   
srv.Databases("AdventureWorks2012").Tables("Person", "Person").Columns("LastName").Alter();   
}  
```  
  
## <a name="iterating-through-the-members-of-a-collection-in-visual-basic"></a>在 Visual Basic 中遍历集合中的成员  
 此代码示例可遍历 <xref:Microsoft.AnalysisServices.Server.Databases%2A> 集合属性并显示数据库与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例之间的所有连接。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBCollections2](SMO How to#SMO_VBCollections2)]  -->  
  
## <a name="iterating-through-the-members-of-a-collection-in-visual-c"></a>在 Visual C# 中遍历集合中的成员  
 此代码示例可遍历 <xref:Microsoft.AnalysisServices.Server.Databases%2A> 集合属性并显示数据库与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例之间的所有连接。  
  
```  
//Connect to the local, default instance of SQL Server.   
{   
Server srv = default(Server);   
srv = new Server();   
int count = 0;   
int total = 0;   
//Iterate through the databases and call the GetActiveDBConnectionCount method.   
Database db = default(Database);   
foreach ( db in srv.Databases) {   
  count = srv.GetActiveDBConnectionCount(db.Name);   
  total = total + count;   
  //Display the number of connections for each database.   
  Console.WriteLine(count + " connections on " + db.Name);   
}   
//Display the total number of connections on the instance of SQL Server.   
Console.WriteLine("Total connections =" + total);   
}   
```  
  
  
