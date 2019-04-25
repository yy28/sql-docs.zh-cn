---
title: 创建、 更改和删除规则 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- rules [SMO]
ms.assetid: 16981459-524e-4b39-a899-4370eaf763cc
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d201b20e0bdfd213c62c060250b5674589ab91cb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62519321"
---
# <a name="creating-altering-and-removing-rules"></a>创建、更改和删除规则
  在 SMO 中，规则由 <xref:Microsoft.SqlServer.Management.Smo.Rule> 对象表示。 规则是由 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.TextBody%2A> 属性进行定义的，该属性是包含使用运算符或谓词（如，IN、LIKE 或 BETWEEN）的条件表达式的文本字符串。 规则不能引用列或其他数据库对象。 可以包括不引用数据库对象的内置函数。  
  
 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.TextBody%2A> 属性中的定义必须包含引用输入的数据值的变量。 可以使用任何名称或符号表示值时创建规则，但第一个字符必须是\@符号。  
  
## <a name="example"></a>示例  
 若要使用所提供的任何代码示例，您必须选择创建应用程序所需的编程环境、编程模板和编程语言。 有关详细信息，请参阅[在 Visual Studio.NET 中创建 Visual Basic SMO 项目](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md)或[创建 Visual C&#35; Visual Studio.NET 中的 SMO 项目](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。  
  
## <a name="creating-altering-and-removing-a-rule-in-visual-basic"></a>在 Visual Basic 中创建、更改和删除规则  
 此代码示例说明如何创建规则，将其附加到列，修改 <xref:Microsoft.SqlServer.Management.Smo.Rule> 对象的属性，从列中分离规则，以及删除规则。  
  
 使用完整的程序集路径指定 <xref:Microsoft.SqlServer.Management.Smo.Rule> 对象的 `Dim` 语句，以便在使用 System.Data 程序集中的 <xref:Microsoft.SqlServer.Management.Smo.Rule> 对象时避免含糊歧义。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBRules1](SMO How to#SMO_VBRules1)]  -->  
  
## <a name="creating-altering-and-removing-a-rule-in-visual-c"></a>在 Visual C# 中创建、更改和删除规则  
 此代码示例说明如何创建规则，将其附加到列，修改 <xref:Microsoft.SqlServer.Management.Smo.Rule> 对象的属性，从列中分离规则，以及删除规则。  
  
 使用完整的程序集路径指定 <xref:Microsoft.SqlServer.Management.Smo.Rule> 对象的 `Dim` 语句，以便在使用 System.Data 程序集中的 <xref:Microsoft.SqlServer.Management.Smo.Rule> 对象时避免含糊歧义。  
  
```  
{  
            //Connect to the local, default instance of SQL Server.   
            Server srv;  
            srv = new Server();  
            //Reference the AdventureWorks2012 database.   
            Database db;  
            db = srv.Databases["AdventureWorks2012"];  
  
            //Define a Rule object variable by supplying the parent database, name and schema in the constructor.   
            //Note that the full namespace must be given for the Rule type to differentiate it from other Rule types.   
            Microsoft.SqlServer.Management.Smo.Rule ru;  
            ru = new Rule(db, "TestRule", "Production");  
            //Set the TextHeader and TextBody properties to define the rule.   
            ru.TextHeader = "CREATE RULE [Production].[TestRule] AS";  
            ru.TextBody = "@value BETWEEN GETDATE() AND DATEADD(year,4,GETDATE())";  
            //Create the rule on the instance of SQL Server.   
            ru.Create();  
            //Bind the rule to a column in the Product table by supplying the table, schema, and   
            //column as arguments in the BindToColumn method.   
            ru.BindToColumn("Product", "SellEndDate", "Production");  
            //Unbind from the column before removing the rule from the database.   
            ru.UnbindFromColumn("Product", "SellEndDate", "Production");  
            ru.Drop();  
  
        }  
```  
  
## <a name="creating-altering-and-removing-a-rule-in-powershell"></a>在 PowerShell 中创建、更改和删除规则  
 此代码示例说明如何创建规则，将其附加到列，修改 <xref:Microsoft.SqlServer.Management.Smo.Rule> 对象的属性，从列中分离规则，以及删除规则。  
  
 使用完整的程序集路径指定 <xref:Microsoft.SqlServer.Management.Smo.Rule> 对象的 `Dim` 语句，以便在使用 System.Data 程序集中的 <xref:Microsoft.SqlServer.Management.Smo.Rule> 对象时避免含糊歧义。  
  
```  
# Set the path context to the local, default instance of SQL Server and get a reference to AdventureWorks2012  
CD \sql\localhost\default\databases  
$db = get-item Adventureworks2012  
  
# Define a Rule object variable by supplying the parent database, name and schema in the constructor.   
$ru = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Rule `  
-argumentlist $db, "TestRule", "Production"  
  
#Set the TextHeader and TextBody properties to define the rule.   
$ru.TextHeader = "CREATE RULE [Production].[TestRule] AS"  
$ru.TextBody = "@value BETWEEN GETDATE() AND DATEADD(year,4,GETDATE())"  
  
#Create the rule on the instance of SQL Server.   
$ru.Create()  
  
# Bind the rule to a column in the Product table by supplying the table, schema, and   
# column as arguments in the BindToColumn method.   
$ru.BindToColumn("Product", "SellEndDate", "Production")  
  
#Unbind from the column before removing the rule from the database.   
$ru.UnbindFromColumn("Product", "SellEndDate", "Production")  
$ru.Drop()  
```  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.SqlServer.Management.Smo.Rule>  
  
  
