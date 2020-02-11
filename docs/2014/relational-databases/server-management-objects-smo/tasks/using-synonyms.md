---
title: 使用同义词 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- synonyms [SMO]
ms.assetid: db0a9022-9549-43e5-b6b3-deb236f05fb8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a96f6ee89b920ec668af21ce625694fc31ce13bd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "72781870"
---
# <a name="using-synonyms"></a>使用同义词
  同义词是架构范围内的对象的另一名称。 在 SMO 中，同义词由 <xref:Microsoft.SqlServer.Management.Smo.Synonym> 对象表示。 
  <xref:Microsoft.SqlServer.Management.Smo.Synonym> 对象是 <xref:Microsoft.SqlServer.Management.Smo.Database> 对象的子对象。 这意味着同义词仅在定义它们的数据库范围内有效。 但是，同义词可以引用位于另一个数据库或 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]远程实例上的对象。  
  
 具有另一名称的对象称为基对象。 
  <xref:Microsoft.SqlServer.Management.Smo.Synonym> 对象的名称属性即为提供给基对象的另一名称。  
  
## <a name="example"></a>示例  
 对于下面的代码示例，您必须选择编程环境、编程模板和编程语言才能创建应用程序。 有关详细信息，请参阅[在 Visual studio .net 中创建 VISUAL BASIC SMO 项目](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md)和[在 visual Studio .Net 中创建 VISUAL C&#35; smo 项目](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。  
  
## <a name="creating-a-synonym-in-visual-basic"></a>在 Visual Basic 中创建同义词  
 代码示例演示了如何为架构范围内的对象创建同义词或备用名称。 通过使用同义词，客户端应用程序可以使用对基对象的单一引用，而不必使用由多部分组成的名称来引用基对象。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBSynonyms1](SMO How to#SMO_VBSynonyms1)]  -->  
  
## <a name="creating-a-synonym-in-visual-c"></a>在 Visual C# 中创建同义词  
 代码示例演示了如何为架构范围内的对象创建同义词或备用名称。 通过使用同义词，客户端应用程序可以使用对基对象的单一引用，而不必使用由多部分组成的名称来引用基对象。  
  
```csharp
{  
            //Connect to the local, default instance of SQL Server.   
            Server srv = new Server();  
  
            //Reference the AdventureWorks2012 database.   
            Database db = srv.Databases["AdventureWorks2012"];  
  
            //Define a Synonym object variable by supplying the   
            //parent database, name, and schema arguments in the constructor.   
            //The name is also a synonym of the name of the base object.   
            Synonym syn = new Synonym(db, "Shop", "Sales");  
  
            //Specify the base object, which is the object on which   
            //the synonym is based.   
            syn.BaseDatabase = "AdventureWorks2012";  
            syn.BaseSchema = "Sales";  
            syn.BaseObject = "Store";  
            syn.BaseServer = srv.Name;  
  
            //Create the synonym on the instance of SQL Server.   
            syn.Create();  
        }  
```  
  
## <a name="creating-a-synonym-in-powershell"></a>在 PowerShell 中创建同义词  
 代码示例演示了如何为架构范围内的对象创建同义词或备用名称。 通过使用同义词，客户端应用程序可以使用对基对象的单一引用，而不必使用由多部分组成的名称来引用基对象。  
  
```powershell
#Get a server object which corresponds to the default instance  
$srv = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
  
#And the database object corresponding to Adventureworks  
$db = $srv.Databases["AdventureWorks2012"]  
  
$syn = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Synonym -ArgumentList $db, "Shop", "Sales"  
  
#Specify the base object, which is the object on which the synonym is based.  
$syn.BaseDatabase = "AdventureWorks2012"  
$syn.BaseSchema = "Sales"  
$syn.BaseObject = "Store"  
$syn.BaseServer = $srv.Name  
  
#Create the synonym on the instance of SQL Server.  
$syn.Create()  
```  
  
## <a name="see-also"></a>另请参阅  
 [CREATE SYNONYM (Transact-SQL)](/sql/t-sql/statements/create-synonym-transact-sql)  
