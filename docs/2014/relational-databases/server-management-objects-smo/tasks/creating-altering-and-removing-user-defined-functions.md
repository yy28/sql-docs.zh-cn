---
title: 创建、 更改和删除用户定义函数 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- user-defined functions [SMO]
ms.assetid: 0ebebd3b-0775-41c2-989d-aa4cf81af12a
caps.latest.revision: 46
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: f7bbe1edc3ce68022f990b441b5c06c737d705e8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36123378"
---
# <a name="creating-altering-and-removing-user-defined-functions"></a>创建、更改和删除用户定义函数
  <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction>对象提供的功能可使用户能以编程方式管理中的用户定义函数[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 用户定义函数支持输入和输出参数，还支持对表列的直接引用。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 需要在这些数据库中注册程序集。 可以使用存储过程中，用户定义函数、 触发器和用户定义数据类型。 SMO 使用 <xref:Microsoft.SqlServer.Management.Smo.SqlAssembly> 对象支持此项功能。  
  
 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction>对象引用.NET 程序集<xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction.AssemblyName%2A>， <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction.ClassName%2A>，和<xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction.MethodName%2A>属性。  
  
 当<xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction>对象引用.NET 程序集，必须通过创建注册该程序集<xref:Microsoft.SqlServer.Management.Smo.SqlAssembly>对象并将其添加到<xref:Microsoft.SqlServer.Management.Smo.SqlAssemblyCollection>了属于对象<xref:Microsoft.SqlServer.Management.Smo.Database>对象。  
  
## <a name="example"></a>示例  
 若要使用所提供的任何代码示例，您必须选择创建应用程序所需的编程环境、编程模板和编程语言。 有关详细信息，请参阅[在 Visual Studio.NET 中创建 Visual Basic SMO 项目](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md)或[创建 Visual C&#35; Visual Studio.NET 中的 SMO 项目](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。  
  
## <a name="creating-a-scalar-user-defined-function-in-visual-basic"></a>在 Visual Basic 中创建标量用户定义函数  
 此代码示例演示如何创建和删除的输入的标量用户定义函数<xref:System.DateTime>对象参数和一个整数返回类型中的[!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]。 在创建用户定义函数[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)]数据库。 该示例创建了用户定义函数 ISOweek，此函数带有一个日期参数，用于计算 ISO 周号。 要使此函数能正确计算，必须在调用此函数之前将数据库 DATEFIRST 选项设置为 1。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBUserDefFuncs1](SMO How to#SMO_VBUserDefFuncs1)]  -->  
  
## <a name="creating-a-scalar-user-defined-function-in-visual-c"></a>在 Visual C# 中创建标量用户定义函数  
 此代码示例演示如何创建和删除的输入的标量用户定义函数<xref:System.DateTime>对象参数和一个整数返回类型中的[!INCLUDE[csprcs](../../../includes/csprcs-md.md)]。 在创建用户定义函数[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)]数据库。 该示例将创建用户定义函数。 `ISOweek`的用户。 此函数使用日期参数来计算 ISO 周数。 要使此函数能正确计算，必须在调用此函数之前将数据库 `DATEFIRST` 选项设置为 `1` 。  
  
```  
{  
            //Connect to the local, default instance of SQL Server.   
           Server srv = new Server();  
            //Reference the AdventureWorks2012 database.   
           Database db = srv.Databases["AdventureWorks2012"];  
  
            //Define a UserDefinedFunction object variable by supplying the parent database and the name arguments in the constructor.   
            UserDefinedFunction udf = new UserDefinedFunction(db, "IsOWeek");  
  
            //Set the TextMode property to false and then set the other properties.   
            udf.TextMode = false;  
            udf.DataType = DataType.Int;  
            udf.ExecutionContext = ExecutionContext.Caller;  
            udf.FunctionType = UserDefinedFunctionType.Scalar;  
            udf.ImplementationType = ImplementationType.TransactSql;  
  
            //Add a parameter.   
  
     UserDefinedFunctionParameter par = new UserDefinedFunctionParameter(udf, "@DATE", DataType.DateTime);  
            udf.Parameters.Add(par);  
  
            //Set the TextBody property to define the user-defined function.   
            udf.TextBody = "BEGIN DECLARE @ISOweek int SET @ISOweek= DATEPART(wk,@DATE)+1 -DATEPART(wk,CAST(DATEPART(yy,@DATE) as CHAR(4))+'0104') IF (@ISOweek=0) SET @ISOweek=dbo.ISOweek(CAST(DATEPART(yy,@DATE)-1 AS CHAR(4))+'12'+ CAST(24+DATEPART(DAY,@DATE) AS CHAR(2)))+1 IF ((DATEPART(mm,@DATE)=12) AND ((DATEPART(dd,@DATE)-DATEPART(dw,@DATE))>= 28)) SET @ISOweek=1 RETURN(@ISOweek) END;";  
  
            //Create the user-defined function on the instance of SQL Server.   
            udf.Create();  
  
            //Remove the user-defined function.   
            udf.Drop();  
        }  
```  
  
## <a name="creating-a-scalar-user-defined-function-in-powershell"></a>在 PowerShell 中创建标量用户定义函数  
 此代码示例演示如何创建和删除的输入的标量用户定义函数<xref:System.DateTime>对象参数和一个整数返回类型中的[!INCLUDE[csprcs](../../../includes/csprcs-md.md)]。 在创建用户定义函数[!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)]数据库。 该示例将创建用户定义函数。 `ISOweek`的用户。 此函数使用日期参数来计算 ISO 周数。 要使此函数能正确计算，必须在调用此函数之前将数据库 `DATEFIRST` 选项设置为 `1` 。  
  
```  
# Set the path context to the local, default instance of SQL Server and get a reference to AdventureWorks2012  
CD \sql\localhost\default\databases  
$db = get-item Adventureworks2012  
  
# Define a user defined function object variable by supplying the parent database and name arguments in the constructor.   
$udf  = New-Object -TypeName Microsoft.SqlServer.Management.SMO.UserDefinedFunction `  
-argumentlist $db, "IsOWeek"  
  
# Set the TextMode property to false and then set the other properties.   
$udf.TextMode = $false  
$udf.DataType = [Microsoft.SqlServer.Management.SMO.DataType]::Int   
$udf.ExecutionContext = [Microsoft.SqlServer.Management.SMO.ExecutionContext]::Caller  
$udf.FunctionType = [Microsoft.SqlServer.Management.SMO.UserDefinedFunctionType]::Scalar  
$udf.ImplementationType = [Microsoft.SqlServer.Management.SMO.ImplementationType]::TransactSql  
  
# Define a Parameter object variable by supplying the parent function, name and type arguments in the constructor.  
$type = [Microsoft.SqlServer.Management.SMO.DataType]::DateTime  
$par  = New-Object -TypeName Microsoft.SqlServer.Management.SMO.UserDefinedFunctionParameter `  
-argumentlist $udf, "@DATE",$type  
  
# Add the parameter to the function  
$udf.Parameters.Add($par)  
  
#Set the TextBody property to define the user-defined function.   
$udf.TextBody = "BEGIN DECLARE @ISOweek int SET @ISOweek= DATEPART(wk,@DATE)+1 -DATEPART(wk,CAST(DATEPART(yy,@DATE) as CHAR(4))+'0104') IF (@ISOweek=0) SET @ISOweek=dbo.ISOweek(CAST(DATEPART(yy,@DATE)-1 AS CHAR(4))+'12'+ CAST(24+DATEPART(DAY,@DATE) AS CHAR(2)))+1 IF ((DATEPART(mm,@DATE)=12) AND ((DATEPART(dd,@DATE)-DATEPART(dw,@DATE))>= 28)) SET @ISOweek=1 RETURN(@ISOweek) END;"  
  
# Create the user-defined function on the instance of SQL Server.   
$udf.Create()  
  
# Remove the user-defined function.   
$udf.Drop()  
```  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunction>  
  
  