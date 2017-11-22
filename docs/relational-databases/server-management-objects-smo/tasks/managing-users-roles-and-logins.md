---
title: "管理用户、 角色和登录名 |Microsoft 文档"
ms.custom: 
ms.date: 08/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: smo
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- logins [SMO]
- roles [SMO]
- users [SMO]
ms.assetid: 74e411fa-74ed-49ec-ab58-68c250f2280e
caps.latest.revision: "45"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: eeda3dc5a30031545b7a6e500c378d6d4c190a6c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="managing-users-roles-and-logins"></a>管理用户、角色和登录名
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]在 SMO 中，登录名由表示<xref:Microsoft.SqlServer.Management.Smo.Login>对象。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中存在登录名时，可将其添加到服务器角色中。 服务器角色由<xref:Microsoft.SqlServer.Management.Smo.ServerRole>对象。 数据库角色由 <xref:Microsoft.SqlServer.Management.Smo.DatabaseRole> 对象表示，而应用程序角色由 <xref:Microsoft.SqlServer.Management.Smo.ApplicationRole> 对象表示。  
  
 与服务器级别关联的权限被列为属性<xref:Microsoft.SqlServer.Management.Smo.ServerPermission>对象。 服务器级别特权可以对各个登录帐户授予、拒绝或从各个登录帐户撤消。  
  
 每个<xref:Microsoft.SqlServer.Management.Smo.Database>对象具有<xref:Microsoft.SqlServer.Management.Smo.UserCollection>指定数据库中的所有用户的对象。 每个用户都与一个登录名相关联。 一个登录名可以与多个数据库中的用户相关联。 <xref:Microsoft.SqlServer.Management.Smo.Login>对象的<xref:Microsoft.SqlServer.Management.Smo.Login.EnumDatabaseMappings%2A>方法可以用于列出与登录相关联的每个数据库中的所有用户。 另外，<xref:Microsoft.SqlServer.Management.Smo.User> 对象的 <xref:Microsoft.SqlServer.Management.Smo.Login> 属性可指定与用户关联的登录名。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]数据库还具有指定一组让用户执行特定任务的数据库级别特权的角色。 与服务器角色不同，数据库角色不是固定的。 可以创建、修改和删除数据库角色。 可以将特权和用户分配给数据库角色以进行大容量管理。  
  
## <a name="example"></a>示例  
 对于下列代码示例，您必须选择编程环境、编程模板和编程语言才能创建应用程序。 有关详细信息，请参阅[创建 Visual C &#35;Visual Studio.NET 中的 SMO 项目](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。  
  
## <a name="enumerating-logins-and-associated-users-in-visual-c"></a>在 Visual C# 中枚举登录名和关联的用户  
 数据库中的每个用户都与一个登录名相关联。 该登录名可以与多个数据库中的用户相关联。 此代码示例说明如何调用 <xref:Microsoft.SqlServer.Management.Smo.Login.EnumDatabaseMappings%2A> 对象的 <xref:Microsoft.SqlServer.Management.Smo.Login> 方法以列出与登录名关联的所有数据库用户。 该示例创建一个登录名和用户在[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)]数据库以确保没有要枚举的映射信息。  
  
```csharp  
{   
Server srv = new Server();   
//Iterate through each database and display.   
  
foreach ( Database db in srv.Databases) {   
   Console.WriteLine("========");   
   Console.WriteLine("Login Mappings for the database: " + db.Name);   
   Console.WriteLine(" ");   
   //Run the EnumLoginMappings method and return details of database user-login mappings to a DataTable object variable.   
   DataTable d;  
   d = db.EnumLoginMappings();   
   //Display the mapping information.   
   foreach (DataRow r in d.Rows) {   
      foreach (DataColumn c in r.Table.Columns) {   
         Console.WriteLine(c.ColumnName + " = " + r[c]);   
      }   
      Console.WriteLine(" ");   
   }   
}   
}  
```  
  
## <a name="enumerating-logins-and-associated-users-in-powershell"></a>在 PowerShell 中枚举登录名和关联的用户  
 数据库中的每个用户都与一个登录名相关联。 该登录名可以与多个数据库中的用户相关联。 此代码示例说明如何调用 <xref:Microsoft.SqlServer.Management.Smo.Login.EnumDatabaseMappings%2A> 对象的 <xref:Microsoft.SqlServer.Management.Smo.Login> 方法以列出与登录名关联的所有数据库用户。 该示例创建一个登录名和用户在[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)]数据库以确保没有要枚举的映射信息。  
  
```powershell  
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\Default\Databases  
  
#Iterate through all databases  
 foreach ($db in Get-ChildItem)  
 {  
 "====="  
 "Login Mappings for the database: "+ $db.Name  
  
 #get the datatable containing the mapping from the smo database oject  
 $dt = $db.EnumLoginMappings()  
  
 #display the results  
 foreach($row in $dt.Rows)  
     {  
        foreach($col in $row.Table.Columns)  
      {  
        $col.ColumnName + "=" + $row[$col]  
       }  
  
     }  
 }  
```  
  
## <a name="managing-roles-and-users"></a>管理角色和用户  
 该示例演示如何管理角色和用户。 若要运行此示例将需要引用以下程序集：  
  
-   Microsoft.SqlServer.Smo.dll  
  
-   Microsoft.SqlServer.Management.Sdk.Sfc.dll  
  
-   Microsoft.SqlServer.ConnectionInfo.dll  
  
-   Microsoft.SqlServer.SqlEnum.dll  
  
```csharp  
using Microsoft.SqlServer.Management.Smo;  
using System;  
  
public class A {  
   public static void Main() {  
      Server svr = new Server();  
      Database db = new Database(svr, "TESTDB");  
      db.Create();  
  
      // Creating Logins  
      Login login = new Login(svr, "Login1");  
      login.LoginType = LoginType.SqlLogin;  
      login.Create("password@1");  
  
      Login login2 = new Login(svr, "Login2");  
      login2.LoginType = LoginType.SqlLogin;  
      login2.Create("password@1");  
  
      // Creating Users in the database for the logins created  
      User user1 = new User(db, "User1");  
      user1.Login = "Login1";  
      user1.Create();  
  
      User user2 = new User(db, "User2");  
      user2.Login = "Login2";  
      user2.Create();  
  
      // Creating database permission Sets  
      DatabasePermissionSet dbPermSet = new DatabasePermissionSet(DatabasePermission.AlterAnySchema);  
      dbPermSet.Add(DatabasePermission.AlterAnyUser);  
  
      DatabasePermissionSet dbPermSet2 = new DatabasePermissionSet(DatabasePermission.CreateType);  
      dbPermSet2.Add(DatabasePermission.CreateSchema);  
      dbPermSet2.Add(DatabasePermission.CreateTable);  
  
      // Creating Database roles  
      DatabaseRole role1 = new DatabaseRole(db, "Role1");  
      role1.Create();  
  
      DatabaseRole role2 = new DatabaseRole(db, "Role2");  
      role2.Create();  
  
      // Granting Database Permission Sets to Roles  
      db.Grant(dbPermSet, role1.Name);  
      db.Grant(dbPermSet2, role2.Name);  
  
      // Adding members (Users / Roles) to Role  
      role1.AddMember("User1");  
  
      role2.AddMember("User2");  
  
      // Role1 becomes a member of Role2  
      role2.AddMember("Role1");  
  
      // Enumerating through explicit permissions granted to Role1  
      // enumerates all database permissions for the Grantee  
      DatabasePermissionInfo[] dbPermsRole1 = db.EnumDatabasePermissions("Role1");     
      foreach (DatabasePermissionInfo dbp in dbPermsRole1) {  
         Console.WriteLine(dbp.Grantee + " has " + dbp.PermissionType.ToString() + " permission.");  
      }  
      Console.WriteLine(" ");  
   }  
}  
```
  
  
