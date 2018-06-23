---
title: Invoke-PolicyEvaluation cmdlet | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Policy-Based Management, Invoke-PolicyEvaluation
- Policy-Based Management, PowerShell
- Invoke-PolicyEvaluation cmdlet
- Cmdlets [SQL Server], Invoke-PolicyEvaluation
- PowerShell [SQL Server], Invoke-PolicyEvaluation
ms.assetid: 3e6d4f5a-59b7-4203-b95a-f7e692c0f131
caps.latest.revision: 18
author: mgblythe
ms.author: mblythe
manager: jhubbard
ms.openlocfilehash: c0ec56b9cde0a2def994d8deffd0ef051459dbf7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36014887"
---
# <a name="invoke-policyevaluation-cmdlet"></a>Invoke-PolicyEvaluation cmdlet
  **Invoke-PolicyEvaluation** 是一个 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] cmdlet，它用于报告 SQL Server 对象的目标集是否符合一个或多个基于策略的管理策略中指定的条件。  
  
## <a name="using-invoke-policyevaluation"></a>使用 Invoke-PolicyEvaluation  
 **Invoke-PolicyEvaluation** 针对一组 SQL Server 对象（称为目标集）评估一个或多个策略。 该组目标对象来自目标服务器。 每个策略都定义一些条件，这些条件是目标对象的允许状态。 例如， **Trustworthy Database** 策略规定 TRUSTWORTHY 数据库属性必须设置为 OFF。  
  
 **-AdHocPolicyEvaluationMode** 参数指定所采取的操作：  
  
 检查  
 使用当前登录名的凭据报告目标对象的策略符合情况。 不重新配置任何对象。 这是默认设置。  
  
 CheckSqlScriptAsProxy  
 使用 **##MS_PolicyTSQLExecutionLogin##** 代理登录名的凭据，报告目标对象的策略符合情况。 不重新配置任何对象。  
  
 配置  
 使用当前登录名的凭据报告目标对象的策略符合情况。 重新配置不符合策略的任何可设置的选项和确定性选项。  
  
## <a name="specifying-polices"></a>指定策略  
 您指定策略的方式取决于策略的存储位置。 策略能够以两种格式存储：  
  
-   它们可以是存储在策略存储区中的对象，例如数据库引擎的实例。 可以使用 SQLSERVER:\SQLPolicy 文件夹指定策略在策略存储区中的位置。 可以使用 Windows PowerShell cmdlet，根据输入策略的属性对其进行筛选，例如使用 Where-Object 来根据策略类别进行筛选，或者使用 Get-Item 根据策略名称进行筛选。  
  
-   它们可以导出为 XML 文件。 可以使用文件系统驱动器（如 D:）指定 XML 文件的位置。 可以使用 Windows PowerShell cmdlet（如 Where-Object），根据策略的文件属性（如文件名）对其进行筛选。  
  
 如果策略存储在策略存储区中，则必须传递一组指向要评估的策略的 PSObject。 通常可以通过将 cmdlet（如 Get-Item）的输出用管道命令发送到 **Invoke-PolicyEvaluation**来完成此操作，并且不需要你指定 **-Policy** 参数。 例如，如果已将 Microsoft 最佳实践策略导入到数据库引擎的实例中，则此命令可评估 **数据库状态** 策略：  
  
```  
sl "SQLSERVER:\SQLPolicy\MyComputer\DEFAULT\Policies"  
Get-Item "Database Status" | Invoke-PolicyEvaluation -TargetServerName "MYCOMPUTER"  
```  
  
 此示例显示如何使用 Where-Object 根据策略的 **PolicyCategory** 属性筛选策略存储区中的多个策略。 **Where-Object** 的管道输出中的对象由 **Invoke-PolicyEvaluation**使用。  
  
```  
sl "SQLSERVER:\SQLPolicy\MyComputer\DEFAULT\Policies"  
gci | Where-Object {$_.PolicyCategory -eq "Microsoft Best Practices: Maintenance"} | Invoke-PolicyEvaluation -TargetServer "MYCOMPUTER"  
```  
  
 如果这些策略存储为 XML 文件，则必须使用 **-Policy** 参数为每个策略提供路径和名称。 如果在 **-Policy** 参数中未指定路径，那么 **Invoke-PolicyEvaulation** 将使用 **sqlps** 路径的当前设置。 例如，此命令根据您登录名的默认数据库评估随 SQL Server 安装的一个 Microsoft 最佳实践策略：  
  
```  
Invoke-PolicyEvaluation -Policy "C:\Program Files\Microsoft SQL Server\120\Tools\Policies\DatabaseEngine\1033\Database Status.xml" -TargetServerName "MYCOMPUTER"  
```  
  
 此命令执行同样的操作，唯一不同的是它使用当前 **sqlps** 路径来指定策略 XML 文件的位置：  
  
```  
sl "C:\Program Files\Microsoft SQL Server\120\Tools\Policies\DatabaseEngine\1033"  
Invoke-PolicyEvaluation -Policy "Database Status.xml" -TargetServerName "MYCOMPUTER"  
```  
  
 此示例显示如何使用 **Get-ChildItem** cmdlet 检索多个策略 XML 文件，并将这些对象用管道命令发送到 **Invoke-PolicyEvaluation**：  
  
```  
sl "C:\Program Files\Microsoft SQL Server\120\Tools\Policies\DatabaseEngine\1033"  
gci "Database Status.xml", "Trustworthy Database.xml" | Invoke-PolicyEvaluation -TargetServer "MYCOMPUTER"  
```  
  
## <a name="specifying-the-target-set"></a>指定目标集  
 使用三个参数指定目标对象集：  
  
-   **-TargetServerName** 指定包含目标对象的 SQL Server 实例。 可在一个字符串中指定这些信息，该字符串应使用为 <xref:System.Data.SqlClient.SqlConnection> 类的 ConnectionString 属性定义的格式。 可以使用 <xref:System.Data.SqlClient.SqlConnectionStringBuilder> 类来生成格式正确的连接字符串。 还可以创建 <xref:Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection> 对象并将其传递到 **-TargetServer**使用。 如果提供只有服务器名称的字符串， **Invoke-PolicyEvaluation** 会使用 Windows 身份验证来连接服务器。  
  
-   **-TargetObjects** 的取值为一个对象或对象数组，它们表示目标集中的 SQL Server 对象。 例如，你可以创建 <xref:Microsoft.SqlServer.Management.Smo.Database> 类对象数组，并将其传递到 **-TargetObjects**使用。  
  
-   **-TargetExpressions** 的取值为一个字符串，其中包含一个指定目标集中对象的查询表达式。 查询表达式的格式是以“/”字符隔开的节点。 每个节点的格式为 ObjectType[Filter]。 ObjectType 是 SQL Server 管理对象 (SMO) 层次结构中的一个对象。 Filter 是一个用于筛选该节点的对象的表达式。 有关详细信息，请参阅 [Query Expressions and Uniform Resource Names](../powershell/query-expressions-and-uniform-resource-names.md)。  
  
 指定 **-TargetObjects** 或 **-TargetExpression**，而不是两者。  
  
 此示例使用 Sfc.SqlStoreConnection 对象指定目标服务器：  
  
```  
sl "C:\Program Files\Microsoft SQL Server\120\Tools\Policies\DatabaseEngine\1033"  
$conn = New-Object Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection("server='MYCOMPUTER';Trusted_Connection=True")  
Invoke-PolicyEvaluation -Policy "Database Status.xml" -TargetServerName $conn  
```  
  
 此示例使用 **-TargetExpression** 标识要评估的特定数据库：  
  
```  
sl "C:\Program Files\Microsoft SQL Server\120\Tools\Policies\DatabaseEngine\1033"  
Invoke-PolicyEvaluation -Policy "Database Status.xml" -TargetServerName "MyComputer" -TargetExpression "Server[@Name='MYCOMPUTER']/Database[@Name='AdventureWorks2012']"  
```  
  
## <a name="evaluating-analysis-services-policies"></a>评估 Analysis Services 策略  
 若要针对 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]实例评估策略，必须在 PowerShell 中加载和注册程序集，使用 Analysis Services 连接对象创建变量，并将该变量传递到 **-TargetObject** 参数。 此示例显示如何评估 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]的最佳实践外围应用配置器策略。  
  
```  
sl "C:\Program Files\Microsoft SQL Server\120\Tools\Policies\AnalysisServices\1033"  
[System.Reflection.Assembly]::LoadWithPartialName("Microsoft.AnalysisServices")  
$SSASsvr = new-object Microsoft.AnalysisServices.Server  
$SSASsvr.Connect("Data Source=Localhost")  
Invoke-PolicyEvaluation -Policy "Surface Area Configuration for Analysis Services Features.xml" -TargetObject $SSASsvr  
```  
  
## <a name="evaluating-reporting-services-policies"></a>评估 Reporting Services 策略  
 若要评估 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 策略，必须在 PowerShell 中加载和注册程序集，使用 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 连接对象创建变量，并将该变量传递到 **-TargetObject** 参数中。 此示例显示如何评估 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]的最佳实践外围应用配置器策略。  
  
```  
sl "C:\Program Files\Microsoft SQL Server\120\Tools\Policies\ReportingServices\1033"  
[System.Reflection.Assembly]::LoadWithPartialName("Microsoft.SqlServer.Dmf.Adapters")  
$SSRSsvr = new-object Microsoft.SqlServer.Management.Adapters.RSContainer('MyComputer')  
Invoke-PolicyEvaluation -Policy "Surface Area Configuration for Reporting Services 2008 Features.xml" -TargetObject $SSRSsvr  
```  
  
## <a name="formatting-output"></a>设置输出的格式  
 默认情况下， **Invoke-PolicyEvaluation** 的输出通过简明报告形式，以可读格式显示在命令提示符窗口中。 可以使用 **-OutputXML** 参数来指定 cmdlet，而不是以 XML 文件形式生成详细报告。 **Invoke-PolicyEvaluation** 使用系统建模语言交换格式 (SML-IF) 架构，因此 SML-IF 读取器可以读取该文件。  
  
```  
sl "SQLSERVER:\SQLPolicy\MyComputer\DEFAULT\Policies"  
Invoke-PolicyEvaluation -Policy "Datbase Status" -TargetServer "MYCOMPUTER" -OutputXML > C:\MyReports\DatabaseStatusReport.xml  
```  
  
## <a name="see-also"></a>请参阅  
 [使用数据库引擎 cmdlet](../../2014/database-engine/use-the-database-engine-cmdlets.md)  
  
  