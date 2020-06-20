---
title: 创建、更改和删除触发器 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- triggers [SMO]
ms.assetid: 8ddbe23b-6e31-4f8e-8a70-17bd5072413e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 13b494e4c2d8d822eb6d25d53d3b50962a65ef49
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85037660"
---
# <a name="creating-altering-and-removing-triggers"></a>创建、更改和删除触发器
  在 SMO 中，触发器由 <xref:Microsoft.SqlServer.Management.Smo.Trigger> 对象表示。 [!INCLUDE[tsql](../../../includes/tsql-md.md)]触发器对象的属性设置所激发的触发器时运行的代码 <xref:Microsoft.SqlServer.Management.Smo.Trigger.TextBody%2A> 。 使用 <xref:Microsoft.SqlServer.Management.Smo.Trigger> 对象的其他属性（如 <xref:Microsoft.SqlServer.Management.Smo.Trigger.Update%2A> 属性）可以设置触发器的类型。 这是一个布尔属性，它指定触发器是否由对父表上的记录所执行的 `UPDATE` 操作激发。  
  
 <xref:Microsoft.SqlServer.Management.Smo.Trigger> 对象表示传统的数据操作语言 (DML) 触发器。 在 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 和更改版本中，也同样支持数据定义语言 (DDL) 触发器。 DDL 触发器由 <xref:Microsoft.SqlServer.Management.Smo.DatabaseDdlTrigger> 对象和 <xref:Microsoft.SqlServer.Management.Smo.ServerDdlTrigger> 对象表示。  
  
## <a name="example"></a>示例  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="creating-altering-and-removing-a-trigger-in-visual-basic"></a>在 Visual Basic 中创建、更改和删除触发器  
 此代码示例演示如何在 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] 数据库中名为 `Sales` 的现有表上创建并插入更新触发器。 当更新表或插入新记录时触发器会发送提醒消息。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBTriggers1](SMO How to#SMO_VBTriggers1)]  -->  
  
## <a name="creating-altering-and-removing-a-trigger-in-visual-c"></a>在 Visual C# 中创建、更改和删除触发器  
 此代码示例演示如何在 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] 数据库中名为 `Sales` 的现有表上创建并插入更新触发器。 当更新表或插入新记录时触发器会发送提醒消息。  
  
```csharp
{  
            //Connect to the local, default instance of SQL Server.   
            Server mysrv;  
            mysrv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database mydb;  
            mydb = mysrv.Databases["AdventureWorks2012"];  
            //Declare a Table object variable and reference the Customer table.   
            Table mytab;  
            mytab = mydb.Tables["Customer", "Sales"];  
            //Define a Trigger object variable by supplying the parent table, schema ,and name in the constructor.   
            Trigger tr;  
            tr = new Trigger(mytab, "Sales");  
            //Set TextMode property to False, then set other properties to define the trigger.   
            tr.TextMode = false;  
            tr.Insert = true;  
            tr.Update = true;  
            tr.InsertOrder = ActivationOrder.First;  
            string stmt;  
            stmt = " RAISERROR('Notify Customer Relations',16,10) ";  
            tr.TextBody = stmt;  
            tr.ImplementationType = ImplementationType.TransactSql;  
            //Create the trigger on the instance of SQL Server.   
            tr.Create();  
            //Remove the trigger.   
            tr.Drop();  
        }  
```  
  
## <a name="creating-altering-and-removing-a-trigger-in-powershell"></a>在 PowerShell 中创建、更改和删除触发器  
 此代码示例演示如何在 [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] 数据库中名为 `Sales` 的现有表上创建并插入更新触发器。 当更新表或插入新记录时触发器会发送提醒消息。  
  
```powershell
# Set the path context to the local, default instance of SQL Server and to the  
#database tables in Adventureworks2012  
CD \sql\localhost\default\databases\AdventureWorks2012\Tables\  
  
#Get reference to the trigger's target table  
$mytab = Get-Item Sales.Customer  
  
# Define a Trigger object variable by supplying the parent table, schema ,and name in the constructor.  
$tr = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Trigger -argumentlist $mytab, "Sales"  
  
# Set TextMode property to False, then set other properties to define the trigger.
$tr.TextMode = $false  
$tr.Insert = $true  
$tr.Update = $true  
$tr.InsertOrder = [Microsoft.SqlServer.Management.SMO.Agent.ActivationOrder]::First  
$tr.TextBody = " RAISERROR('Notify Customer Relations',16,10) "  
$tr.ImplementationType = [Microsoft.SqlServer.Management.SMO.ImplementationType]::TransactSql  
  
# Create the trigger on the instance of SQL Server.
$tr.Create()  
  
#Remove the trigger.
$tr.Drop()  
```  
