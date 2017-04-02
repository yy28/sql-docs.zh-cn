---
title: "Remove-RoleMember cmdlet | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: e38f56ab-facd-4bef-9502-f52f8486a6a6
caps.latest.revision: 8
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 8
---
# Remove-RoleMember cmdlet
  从 Analysis Services 数据库的指定角色中删除成员。  
  
## 语法  
 `Remove-RoleMember [-MemberName] <System.String> [-Database] <System.String> [-RoleName] <System.String> [<CommonParameters>]`  
  
 `Remove-RoleMember [-DatabaseRole] <Microsoft.AnalysisServices.Role> [-MemberName] <System.String>  [<CommonParameters>]`  
  
## Description  
 Remove-RoleMember cmdlet 从 Analysis Services 数据库的角色中删除现有成员。  
  
## Parameters  
  
### -MemberName \<string>  
 指定要从角色中删除的 Windows 用户或组。  
  
|||  
|-|-|  
|必需？|true|  
|位置？|0|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### -Database \<string>  
 指定角色属于的数据库。  
  
|||  
|-|-|  
|必需？|true|  
|位置？|1|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### -RoleName \<string>  
 指定要从其删除成员的角色。  
  
|||  
|-|-|  
|必需？|true|  
|位置？|2|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### -DatabaseRole \<string>  
 指定要从其删除成员的 Microsoft.AnalysisServices.Role 对象。 在您想要通过管道来提供数据库角色时，可以使用此参数来代替–Database 和 –RoleName 参数。  
  
|||  
|-|-|  
|必需？|true|  
|位置？|所指定位置|  
|默认值||  
|接受管道输入？|true (ByPropertyName)|  
|接受通配符？|false|  
  
### \<CommonParameters>  
 此 cmdlet 支持以下常用参数：-Verbose、-Debug、-ErrorAction、-ErrorVariable、-OutBuffer 和 -OutVariable。 有关详细信息，请参阅 [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825)。  
  
## 输入和输出  
 无。  
  
## 示例 1  
  
```  
PS SQLSERVER:\sqlas\localhost\default> remove-rolemember –membername “adventure-works\bobh” –database “AdventureWorks” –rolename “Reader”  
```  
  
 对于正在本地默认实例上运行的 AdventureWorks 数据库，此命令将从读取者角色中删除一个 Windows 域用户帐户。  
  
## 示例 2  
  
```  
PS SQLSERVER:\sqlas\localhost\default> $roles= dir .\databases\AWTEST\Roles  
PS SQLSERVER:\sqlas\localhost\default> $roles  
PS SQLSERVER:\sqlas\localhost\default> remove-rolemember –membername:“adventure-works\bobh” –databaserole:$roles[0]  
```  
  
 第 1 行将 AWTEST 数据库的所有数据库角色添加到管道。 第 2 行（您在提示符处键入 $roles）显示角色数组。 第 3 行将从该数组中删除 Windows 用户“adventure-works\bobh”。  
  
## 示例 3  
  
```  
PS SQLSERVER:\sqlas\localhost\default\Databases\AWTEST\Roles> $roles=dir  
PS SQLSERVER:\sqlas\localhost\default\Databases\AWTEST\Roles> $roles[0] | Remove-rolemember –membername “adventure-works\bobh”  
```  
  
 此命令将从某一数组中的第一个角色上删除一个 Windows 域用户帐户，该数组是通过列出特定数据库 (AWTEST) 的上下文中 Roles 文件夹的子级创建的。  
  
## 另请参阅  
 [PowerShell scripting in Analysis Services](../../analysis-services/instances/powershell-scripting-in-analysis-services.md)   
 [使用 PowerShell 管理表格模型](http://go.microsoft.com/fwlink/?linkID=227685)  
  
  