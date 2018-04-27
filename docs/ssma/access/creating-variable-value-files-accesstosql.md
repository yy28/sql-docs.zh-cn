---
title: 创建变量值文件 (AccessToSQL) |Microsoft 文档
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-access
ms.custom: ''
ms.date: 08/17/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 808595c3-8ef1-40bd-a93e-5cf237950e08
caps.latest.revision: 15
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a216202893e40bfd4a3c1e960fba9db1c08f809c
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="creating-variable-value-files-accesstosql"></a>创建变量值文件 (AccessToSQL)
变量的值文件是 XML 文件包含频繁更改跨服务器迁移的命令 （例如源或目标服务器名称） 的参数值。 大量的数据库迁移发生时，多个变量的文件，用于存储每个源服务器的值都是创建，并且在主脚本文件与引用**– v**切换在命令行。 此行为有助于维护几个脚本文件中的多个变量的文件中的变量值的静态值。  
  
> [!NOTE]  
> -  变量名是前缀和后缀，以 $ （美元） 符号。 如果变量的值文件中的值，而不分配的变量，分析脚本文件的过程将会出错，导致停滞控制台执行过程。  
> -  The escape character for **$** is **$$**. 如果一个变量或静态参数的值的值包含**$** （美元） 符号，然后**$$** 必须指定将其视为字符而不是变量。  
> -  出于可维护性目的，可以在声明变量`‘variable-group’`逻辑分隔的用户定义的变量的元素。  此元素的使用情况不是必需的。  
  
**示例：**  
  
**示例 1:**  
  
```xml  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="ProjectSpecs">  
  
    <variable name="$type$" value="MyProject"/>  
  
    <variable name="$project_folder$" value=".\$project_name$"/>  
  
    <variable name="$project_name$" value="$type$ConsoleProject"/>  
  
    <variable name="$project_overwrite$" value="true"/>  
  
    <variable name="$project_type$" value="sql-server-2008"/>  
  
  </variable-group>  
  
</variables>  
```  
**示例 2:**  
  
```xml  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="SQLServerParams">  
  
    <variable-group name="SqlServerConnectionParams">  
  
      <variable name="$TargetServerName$" value="xxx"/>  
  
      <variable name="$TargetDB$" value="xxx"/>  
  
      <variable name="$TargetUserName$" value="xxx"/>  
  
      <variable name="$TargetPassword$" value="xxx"/>  
  
      <variable name="$TargetIsTrusted$" value="xxx"/>  
  
      <variable name="$TrustedConnection$" value="xxx"/>  
  
    </variable-group>  
  
    <variable-group name="SqlServerObjectParams">  
  
      <variable name="$ObjectName1$" value="TestTable1"/>  
  
      <variable name="$ObjectName2$" value="TestProc1"/>  
  
    </variable-group>  
  
  </variable-group>  
  
</variables>  
```  
  
## <a name="variable-value-file-validation"></a>变量值文件验证  
用户可以轻松地验证他/她变量值文件是否符合的架构定义文件**ConsoleScriptVariablesSchema.xsd**架构文件夹中可用。  
  
## <a name="next-step"></a>下一步  
操作控制台的下一步是[服务器连接文件创建&#40;AccessToSQL&#41;](../../ssma/access/creating-the-server-connection-files-accesstosql.md)  
  
## <a name="see-also"></a>另请参阅  
[创建服务器连接文件 (Access)](http://msdn.microsoft.com/829153be-aa8e-4162-87e8-69882feecf19)  
  
