---
title: "删除了 cmdlet |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: e38f56ab-facd-4bef-9502-f52f8486a6a6
caps.latest.revision: 8
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c093787d86398acaaeaca8f282e1f588c3e726d7
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="remove-rolemember-cmdlet"></a>Remove-RoleMember cmdlet

[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  从 Analysis Services 数据库的指定角色中删除成员。  

>[!NOTE] 
>这篇文章可能包含过期的信息和示例。 有关最新的使用 Get-help cmdlet。
  
## <a name="syntax"></a>语法  
 `Remove-RoleMember [-MemberName] <System.String> [-Database] <System.String> [-RoleName] <System.String> [<CommonParameters>]`  
  
 `Remove-RoleMember [-DatabaseRole] <Microsoft.AnalysisServices.Role> [-MemberName] <System.String>  [<CommonParameters>]`  
  
## <a name="description"></a>Description  
 Remove-RoleMember cmdlet 从 Analysis Services 数据库的角色中删除现有成员。  
  
## <a name="parameters"></a>Parameters  
  
### <a name="-membername-string"></a>-MemberName\<字符串 >  
 指定要从角色中删除的 Windows 用户或组。  
  
|||  
|-|-|  
|必需？|true|  
|位置？|0|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-database-string"></a>-数据库\<字符串 >  
 指定角色属于的数据库。  
  
|||  
|-|-|  
|必需？|true|  
|位置？|1|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-rolename-string"></a>-RoleName\<字符串 >  
 指定要从其删除成员的角色。  
  
|||  
|-|-|  
|必需？|true|  
|位置？|2|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-databaserole-string"></a>-DatabaseRole\<字符串 >  
 指定要从其删除成员的 Microsoft.AnalysisServices.Role 对象。 在您想要通过管道来提供数据库角色时，可以使用此参数来代替–Database 和 –RoleName 参数。  
  
|||  
|-|-|  
|必需？|true|  
|位置？|所指定位置|  
|默认值||  
|接受管道输入？|true (ByPropertyName)|  
|接受通配符？|false|  
  
### <a name="commonparameters"></a>\<CommonParameters >  
 此 cmdlet 支持以下常用参数：-Verbose、-Debug、-ErrorAction、-ErrorVariable、-OutBuffer 和 -OutVariable。 有关详细信息，请参阅 [About_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825)。  
  
## <a name="inputs-and-outputs"></a>输入和输出  
 无。  
  
## <a name="example-1"></a>示例 1  
  
```  
PS SQLSERVER:\sqlas\localhost\default> remove-rolemember –membername “adventure-works\bobh” –database “AdventureWorks” –rolename “Reader”  
```  
  
 对于正在本地默认实例上运行的 AdventureWorks 数据库，此命令将从读取者角色中删除一个 Windows 域用户帐户。  
  
## <a name="example-2"></a>示例 2  
  
```  
PS SQLSERVER:\sqlas\localhost\default> $roles= dir .\databases\AWTEST\Roles  
PS SQLSERVER:\sqlas\localhost\default> $roles  
PS SQLSERVER:\sqlas\localhost\default> remove-rolemember –membername:“adventure-works\bobh” –databaserole:$roles[0]  
```  
  
 第 1 行将 AWTEST 数据库的所有数据库角色添加到管道。 第 2 行（您在提示符处键入 $roles）显示角色数组。 第 3 行将从该数组中删除 Windows 用户“adventure-works\bobh”。  
  
## <a name="example-3"></a>示例 3  
  
```  
PS SQLSERVER:\sqlas\localhost\default\Databases\AWTEST\Roles> $roles=dir  
PS SQLSERVER:\sqlas\localhost\default\Databases\AWTEST\Roles> $roles[0] | Remove-rolemember –membername “adventure-works\bobh”  
```  
  
 此命令将从某一数组中的第一个角色上删除一个 Windows 域用户帐户，该数组是通过列出特定数据库 (AWTEST) 的上下文中 Roles 文件夹的子级创建的。  
  

  
  

