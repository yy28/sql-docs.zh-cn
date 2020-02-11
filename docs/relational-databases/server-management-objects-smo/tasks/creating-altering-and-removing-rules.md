---
title: 创建、更改和删除规则
ms.custom: seo-dt-2019
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- rules [SMO]
ms.assetid: 16981459-524e-4b39-a899-4370eaf763cc
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b2f918e611a4bc88c1a77ad7d539a9101f3f8dac
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "74095530"
---
# <a name="creating-altering-and-removing-rules"></a>创建、更改和删除规则
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  在 SMO 中，规则由 <xref:Microsoft.SqlServer.Management.Smo.Rule> 对象表示。 规则是由 <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.TextBody%2A> 属性进行定义的，该属性是包含使用运算符或谓词（如，IN、LIKE 或 BETWEEN）的条件表达式的文本字符串。 规则不能引用列或其他数据库对象。 可以包括不引用数据库对象的内置函数。  
  
 
  <xref:Microsoft.SqlServer.Management.Smo.DefaultRuleBase.TextBody%2A> 属性中的定义必须包含引用输入的数据值的变量。 创建规则时，可以使用任何名称或符号表示值，但第一个字符必须是\@符号。  
  
## <a name="example"></a>示例  
 若要使用所提供的任何代码示例，您必须选择创建应用程序所需的编程环境、编程模板和编程语言。 有关详细信息，请参阅[在 Visual Studio .net 中创建 Visual C&#35; SMO 项目](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。  
  
## <a name="creating-altering-and-removing-a-rule-in-visual-basic"></a>在 Visual Basic 中创建、更改和删除规则  
 此代码示例说明如何创建规则，将其附加到列，修改 <xref:Microsoft.SqlServer.Management.Smo.Rule> 对象的属性，从列中分离规则，以及删除规则。  
  
 为**** <xref:Microsoft.SqlServer.Management.Smo.Rule>对象指定 Dim 语句时使用完整的程序集路径，以避免对 system.web 程序<xref:Microsoft.SqlServer.Management.Smo.Rule>集中的对象产生歧义。  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Reference the AdventureWorks2012 database.
Dim db As Database
db = srv.Databases("AdventureWorks2012")
'Declare a Table object variable and reference the Product table.
Dim tb As Table
tb = db.Tables("Product", "Production")
'Define a Rule object variable by supplying the parent database, name and schema in the constructor. 
'Note that the full namespace must be given for the Rule type to differentiate it from other Rule types.
Dim ru As Microsoft.SqlServer.Management.Smo.Rule
ru = New Rule(db, "TestRule", "Production")
'Set the TextHeader and TextBody properties to define the rule.
ru.TextHeader = "CREATE RULE [Production].[TestRule] AS"
ru.TextBody = "@value BETWEEN GETDATE() AND DATEADD(year,4,GETDATE())"
'Create the rule on the instance of SQL Server.
ru.Create()
'Bind the rule to a column in the Product table by supplying the table, schema, and 
'column as arguments in the BindToColumn method.
ru.BindToColumn("Product", "SellEndDate", "Production")
'Unbind from the column before removing the rule from the database.
ru.UnbindFromColumn("Product", "SellEndDate", "Production")
ru.Drop()
```
  
## <a name="creating-altering-and-removing-a-rule-in-visual-c"></a>在 Visual C# 中创建、更改和删除规则  
 此代码示例说明如何创建规则，将其附加到列，修改 <xref:Microsoft.SqlServer.Management.Smo.Rule> 对象的属性，从列中分离规则，以及删除规则。  
  
 为**** <xref:Microsoft.SqlServer.Management.Smo.Rule>对象指定 Dim 语句时使用完整的程序集路径，以避免对 system.web 程序<xref:Microsoft.SqlServer.Management.Smo.Rule>集中的对象产生歧义。  
  
```csharp  
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
  
 为**** <xref:Microsoft.SqlServer.Management.Smo.Rule>对象指定 Dim 语句时使用完整的程序集路径，以避免对 system.web 程序<xref:Microsoft.SqlServer.Management.Smo.Rule>集中的对象产生歧义。  
  
```powershell   
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
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.SqlServer.Management.Smo.Rule>  
  
  
