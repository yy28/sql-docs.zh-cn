---
title: 添加了 cmdlet |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: powershell
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8144e76d8d3ba7e0ff588c9f22875af430b68a1b
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34031910"
---
# <a name="add-rolemember-cmdlet"></a>Add-RoleMember cmdlet
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]

  将成员添加到 Analysis Services 表格或多维数据库的指定角色。  

>[!NOTE] 
>这篇文章可能包含过期的信息和示例。 有关最新的使用 Get-help cmdlet。
  
## <a name="syntax"></a>语法  
 `Add-RoleMember [-MemberName] <System.String> [-Database] <System.String> [-RoleName] <System.String> [<CommonParameters>]`  
  
 `Add-RoleMember [-MemberName] <System.String> [-DatabaseRole] <Microsoft.AnalysisServices.Role> [<CommonParameters>]`  
  
## <a name="description"></a>Description  
 Add-RoleMember cmdlet 将有效成员添加到现有数据库角色。 仅允许数据库角色。 不能使用此 cmdlet 向服务器角色添加成员。  
  
 一次只能添加一个成员，该成员可以是用户或组帐户。  
  
## <a name="parameters"></a>Parameters  
  
### <a name="-membername-string"></a>-MemberName\<字符串 >  
 指定要添加到该角色的 Windows 用户或组。  
  
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
 指定要将成员添加到的角色。  
  
|||  
|-|-|  
|必需？|true|  
|位置？|2|  
|默认值||  
|接受管道输入？|false|  
|接受通配符？|false|  
  
### <a name="-databaserole-string"></a>-DatabaseRole\<字符串 >  
 指定成员应该添加到的 Microsoft.AnalysisServices.Role 对象。 在您想要通过管道来提供数据库角色时，可以使用此参数来代替–Database 和 –RoleName 参数。  
  
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
 输入类型是可以传送到 cmdlet 的对象的类型。 返回类型是 cmdlet 所返回的对象的类型。  
  
|||  
|-|-|  
|输入|无。|  
|输出|InclusionThresholdSetting|  
  
## <a name="example-1"></a>示例 1  
  
```  
PS SQLSERVER:\sqlas\localhost\default> add-rolemember –membername “adventure-works\bobh” –database “AdventureWorks” –rolename “Reader”  
```  
  
 对于在本地默认实例上运行的 AdventureWorks 数据库，此命令将一个 Windows 域用户帐户添加到读取者角色。  
  
## <a name="example-2"></a>示例 2  
  
```  
PS SQLSERVER:\sqlas\localhost\default> $roles= dir .\databases\AWTEST\Roles  
PS SQLSERVER:\sqlas\localhost\default> $roles  
PS SQLSERVER:\sqlas\localhost\default> add-rolemember –membername:“adventure-works\bobh” –databaserole:$roles[0]  
```  
  
 第 1 行将 AWTEST 数据库的所有数据库角色添加到管道。 第 2 行（您在提示符处键入 $roles）显示角色数组。 第 3 行将 Windows 用户 adventure-works\bobh 作为第一个角色的成员添加到该数组中。  
  
## <a name="example-3"></a>示例 3  
  
```  
PS SQLSERVER:\sqlas\localhost\default\Databases\AWTEST\Roles> $roles=dir  
PS SQLSERVER:\sqlas\localhost\default\Databases\AWTEST\Roles> $roles[0] | Add-rolemember –membername “adventure-works\bobh”  
```  
  
 此命令将一个 Windows 域用户帐户添加到某一数组中的第一个角色上，该数组是通过列出特定数据库 (AWTEST) 的上下文中 Roles 文件夹的子级创建的。  
  

  
  
