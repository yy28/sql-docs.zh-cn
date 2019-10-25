---
title: 创建、更改和删除外键 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- foreign keys [SMO]
ms.assetid: d43c8dca-bb6b-4a41-8a79-c96fd546fc91
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a0462af67afbf5ac25c52ded8523ca26678699b9
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/23/2019
ms.locfileid: "72796955"
---
# <a name="creating-altering-and-removing-foreign-keys"></a>创建、更改和删除外键
  在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 管理对象 (SMO) 中，外键由 <xref:Microsoft.SqlServer.Management.Smo.ForeignKey> 对象表示。  
  
 若要在 SMO 中创建外键，则必须在 <xref:Microsoft.SqlServer.Management.Smo.ForeignKey> 对象的构造函数中指定在其上定义外键的表。 在该表中，必须至少选择一个列作为外键。 为此，请创建一个 <xref:Microsoft.SqlServer.Management.Smo.ForeignKeyColumn> 对象变量并指定作为外键的列的名称。 然后指定被引用表和被引用列。 使用 <xref:Microsoft.SqlServer.Management.Smo.ForeignKeyColumnCollection.Add%2A> 方法将列添加到 `Columns` 对象属性。  
  
 表示外键的列在 <xref:Microsoft.SqlServer.Management.Smo.ForeignKey> 对象的 `Columns` 对象属性中列出。 外键引用的主键由在 <xref:Microsoft.SqlServer.Management.Smo.ForeignKey.ReferencedKey%2A> 属性中指定的表中的 <xref:Microsoft.SqlServer.Management.Smo.ForeignKey.ReferencedTable%2A> 属性表示。  
  
## <a name="example"></a>示例  
 若要使用所提供的任何代码示例，您必须选择创建应用程序所需的编程环境、编程模板和编程语言。 有关详细信息，请参阅[在 Visual studio .net 中创建 VISUAL BASIC SMO 项目](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md)或[在 visual Studio&#35; .Net 中创建 visual C SMO 项目](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。  
  
## <a name="creating-altering-and-removing-a-foreign-key-in-visual-basic"></a>在 Visual Basic 中创建、更改和删除外键  
 此代码示例演示如何在一个表的一个或多个列与另一个表的主键列之间创建外键关系。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBForeignKeys1](SMO How to#SMO_VBForeignKeys1)]  -->  
  
## <a name="creating-altering-and-removing-a-foreign-key-in-visual-c"></a>在 Visual C# 中创建、更改和删除外键  
 此代码示例演示如何在一个表的一个或多个列与另一个表的主键列之间创建外键关系。  
  
```csharp
{  
            //Connect to the local, default instance of SQL Server.   
            Server srv;  
            srv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database db;  
            db = srv.Databases["AdventureWorks2012"];  
            //Declare another Table object variable and reference the EmployeeDepartmentHistory table.   
            Table tbea;  
            tbea = db.Tables["EmployeeDepartmentHistory", "HumanResources"];  
            //Define a Foreign Key object variable by supplying the EmployeeDepartmentHistory as the parent table and the foreign key name in the constructor.   
            ForeignKey fk;  
            fk = new ForeignKey(tbea, "test_foreignkey");  
            //Add BusinessEntityID as the foreign key column.   
            ForeignKeyColumn fkc;  
            fkc = new ForeignKeyColumn(fk, "BusinessEntityID", "BusinessEntityID");  
            fk.Columns.Add(fkc);  
            //Set the referenced table and schema.   
            fk.ReferencedTable = "Employee";  
            fk.ReferencedTableSchema = "HumanResources";  
            //Create the foreign key on the instance of SQL Server.   
            fk.Create();  
        }  
```  
  
## <a name="creating-altering-and-removing-a-foreign-key-in-powershell"></a>在 PowerShell 中创建、更改和删除外键  
 此代码示例演示如何在一个表的一个或多个列与另一个表的主键列之间创建外键关系。  
  
```powershell
# Set the path context to the local, default instance of SQL Server and to the  
#database tables in Adventureworks2012  
CD \sql\localhost\default\databases\AdventureWorks2012\Tables\  
  
#Get reference to the FK table  
$tbea = get-item HumanResources.EmployeeDepartmentHistory  
  
# Define a Foreign Key object variable by supplying the EmployeeDepartmentHistory  
# as the parent table and the foreign key name in the constructor.   
$fk = New-Object -TypeName Microsoft.SqlServer.Management.SMO.ForeignKey `  
-argumentlist $tbea, "test_foreignkey"  
  
#Add BusinessEntityID as the foreign key column.   
$fkc = New-Object -TypeName Microsoft.SqlServer.Management.SMO.ForeignKeyColumn `  
-argumentlist $fk, "BusinessEntityID", "BusinessEntityID"  
$fk.Columns.Add($fkc)  
  
#Set the referenced table and schema.   
$fk.ReferencedTable = "Employee"  
$fk.ReferencedTableSchema = "HumanResources"  
  
#Create the foreign key on the instance of SQL Server.   
$fk.Create()  
```  
  
## <a name="sample-foreign-keys-primary-keys-and-unique-constraint-columns"></a>示例：外键、主键和唯一约束列  
 本示例演示：  
  
-   在现有对象上查找外键。  
  
-   如何创建主键。  
  
-   如何创建唯一约束列。  
  
 此示例的 C# 版本：  
  
```csharp
// compile with:   
// /r:Microsoft.SqlServer.Smo.dll   
// /r:microsoft.sqlserver.management.sdk.sfc.dll   
// /r:Microsoft.SqlServer.ConnectionInfo.dll  
// /r:Microsoft.SqlServer.SqlEnum.dll  
  
using Microsoft.SqlServer.Management.Smo;  
using Microsoft.SqlServer.Management.Sdk.Sfc;  
using Microsoft.SqlServer.Management.Common;  
using System;  
  
public class A {  
   public static void Main() {  
      Server svr = new Server();  
      Database db = new Database(svr, "TESTDB");  
      db.Create();  
  
      // PK Table  
      Table tab1 = new Table(db, "Table1");  
  
      // Define Columns and add them to the table  
      Column col1 = new Column(tab1, "Col1", DataType.Int);  
  
      col1.Nullable = false;  
      tab1.Columns.Add(col1);  
      Column col2 = new Column(tab1, "Col2", DataType.NVarChar(50));  
      tab1.Columns.Add(col2);  
      Column col3 = new Column(tab1, "Col3", DataType.DateTime);  
      tab1.Columns.Add(col3);  
  
      // Create the ftable  
      tab1.Create();  
  
      // Define Index object on the table by supplying the Table1 as the parent table and the primary key name in the constructor.  
      Index pk = new Index(tab1, "Table1_PK");  
      pk.IndexKeyType = IndexKeyType.DriPrimaryKey;  
  
      // Add Col1 as the Index Column  
      IndexedColumn idxCol1 = new IndexedColumn(pk, "Col1");  
      pk.IndexedColumns.Add(idxCol1);  
  
      // Create the Primary Key  
      pk.Create();  
  
      // Create Unique Index on the table  
      Index unique = new Index(tab1, "Table1_Unique");  
      unique.IndexKeyType = IndexKeyType.DriUniqueKey;  
  
      // Add Col1 as the Unique Index Column  
      IndexedColumn idxCol2 = new IndexedColumn(unique, "Col2");  
      unique.IndexedColumns.Add(idxCol2);  
  
      // Create the Unique Index  
      unique.Create();  
  
      // Create Table2                    
      Table tab2 = new Table(db, "Table2");  
      Column col21 = new Column(tab2, "Col21", DataType.NChar(20));  
      tab2.Columns.Add(col21);  
      Column col22 = new Column(tab2, "Col22", DataType.Int);  
      tab2.Columns.Add(col22);  
      tab2.Create();  
  
      // Define a Foreign Key object variable by supplying the Table2 as the parent table and the foreign key name in the constructor.   
      ForeignKey fk = new ForeignKey(tab2, "Table2_FK");  
  
      // Add Col22 as the foreign key column.   
      ForeignKeyColumn fkc = new ForeignKeyColumn(fk, "Col22", "Col1");  
      fk.Columns.Add(fkc);  
      fk.ReferencedTable = "Table1";  
  
      // Create the foreign key on the instance of SQL Server.   
      fk.Create();                    
  
      // Get list of Foreign Keys on Table2  
      foreach (ForeignKey f in tab2.ForeignKeys) {  
            Console.WriteLine(f.Name + " " + f.ReferencedTable + " " + f.ReferencedKey);  
      }  
  
      // Get list of Foreign Keys referencing table1  
      foreach (Table tab in db.Tables) {  
         if (tab == tab1)  
            continue;  
            foreach (ForeignKey f in tab.ForeignKeys) {  
               if (f.ReferencedTable.Equals(tab1.Name))  
                  Console.WriteLine(f.Name + " " + f.Parent.Name);  
            }  
      }  
   }  
}  
```  
  
 此示例的 Visual Basic 版本：  
  
```vb
' compile with:   
' /r:Microsoft.SqlServer.Smo.dll   
' /r:microsoft.sqlserver.management.sdk.sfc.dll   
' /r:Microsoft.SqlServer.ConnectionInfo.dll  
' /r:Microsoft.SqlServer.SqlEnum.dll  
  
Imports Microsoft.SqlServer.Management.Smo  
Imports Microsoft.SqlServer.Management.Sdk.Sfc  
Imports Microsoft.SqlServer.Management.Common  
  
Public Class A  
   Public Shared Sub Main()  
      Dim svr As New Server()  
      Dim db As New Database(svr, "TESTDB")  
      db.Create()  
  
      ' PK Table  
      Dim tab1 As New Table(db, "Table1")  
  
      ' Define Columns and add them to the table  
      Dim col1 As New Column(tab1, "Col1", DataType.Int)  
  
      col1.Nullable = False  
      tab1.Columns.Add(col1)  
      Dim col2 As New Column(tab1, "Col2", DataType.NVarChar(50))  
      tab1.Columns.Add(col2)  
      Dim col3 As New Column(tab1, "Col3", DataType.DateTime)  
      tab1.Columns.Add(col3)  
  
      ' Create the ftable  
      tab1.Create()  
  
      ' Define Index object on the table by supplying the Table1 as the parent table and the primary key name in the constructor.  
      Dim pk As New Index(tab1, "Table1_PK")  
      pk.IndexKeyType = IndexKeyType.DriPrimaryKey  
  
      ' Add Col1 as the Index Column  
      Dim idxCol1 As New IndexedColumn(pk, "Col1")  
      pk.IndexedColumns.Add(idxCol1)  
  
      ' Create the Primary Key  
      pk.Create()  
  
      ' Create Unique Index on the table  
      Dim unique As New Index(tab1, "Table1_Unique")  
      unique.IndexKeyType = IndexKeyType.DriUniqueKey  
  
      ' Add Col1 as the Unique Index Column  
      Dim idxCol2 As New IndexedColumn(unique, "Col2")  
      unique.IndexedColumns.Add(idxCol2)  
  
      ' Create the Unique Index  
      unique.Create()  
  
      ' Create Table2                    
      Dim tab2 As New Table(db, "Table2")  
      Dim col21 As New Column(tab2, "Col21", DataType.NChar(20))  
      tab2.Columns.Add(col21)  
      Dim col22 As New Column(tab2, "Col22", DataType.Int)  
      tab2.Columns.Add(col22)  
      tab2.Create()  
  
      ' Define a Foreign Key object variable by supplying the Table2 as the parent table and the foreign key name in the constructor.   
      Dim fk As New ForeignKey(tab2, "Table2_FK")  
  
      ' Add Col22 as the foreign key column.   
      Dim fkc As New ForeignKeyColumn(fk, "Col22", "Col1")  
      fk.Columns.Add(fkc)  
      fk.ReferencedTable = "Table1"  
  
      ' Create the foreign key on the instance of SQL Server.   
      fk.Create()  
  
      ' Get list of Foreign Keys on Table2  
      For Each f As ForeignKey In tab2.ForeignKeys  
         Console.WriteLine((f.Name + " " + f.ReferencedTable & " ") + f.ReferencedKey)  
      Next  
  
      ' Get list of Foreign Keys referencing table1  
      For Each tab As Table In db.Tables  
         If (tab.Name.Equals(tab1.Name)) Then  
            Continue For  
         End If  
         For Each f As ForeignKey In tab.ForeignKeys  
            If f.ReferencedTable.Equals(tab1.Name) Then  
               Console.WriteLine(f.Name + " " + f.Parent.Name)  
            End If  
         Next  
      Next  
   End Sub  
End Class  
```  
