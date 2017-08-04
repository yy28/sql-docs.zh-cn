---
title: "创建变量值文件 (AccessToSQL) |Microsoft 文档"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 808595c3-8ef1-40bd-a93e-5cf237950e08
caps.latest.revision: 15
author: sabotta
ms.author: carlasab
manager: lonnyb
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2ebc00ea1b5fc7eb9ca2383d8887b522f59428d1
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="creating-variable-value-files-accesstosql"></a>创建变量值文件 (AccessToSQL)
变量的值文件是 XML 文件包含频繁更改从一台服务器迁移到另一个类似的源或目标服务器名称的命令的参数值。 多个变量的文件，用于存储每个源服务器的值时将发生大量的数据库迁移，将创建并中的主脚本文件引用**– v**切换在命令行。 这有助于在维护几个脚本文件中的多个变量的文件中的变量值的静态值。  
  
> [!NOTE]  
> 1.  变量名是前缀和后缀，以 $ （美元） 符号。 如果变量未分配的变量值文件中的值，将导致停止控制台执行过程的脚本文件的分析过程中遇到错误。  
> 2.  The escape character for **$** is **$$**. 如果一个变量或静态参数的值的值包含 **$**  （美元） 符号，然后 **$$** 必须指定将其视为字符而不是变量。  
> 3.  出于可维护性目的，可以在声明变量`‘variable-group’`的用户的逻辑分隔的元素定义的变量。  此元素的使用情况不是必需的。  
  
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
操作控制台的下一步是[创建服务器连接文件 &#40;AccessToSQL &#41;](../../ssma/access/creating-the-server-connection-files-accesstosql.md)  
  
## <a name="see-also"></a>另請參閱  
[创建服务器连接文件 (Access)](http://msdn.microsoft.com/en-us/829153be-aa8e-4162-87e8-69882feecf19)  
  

