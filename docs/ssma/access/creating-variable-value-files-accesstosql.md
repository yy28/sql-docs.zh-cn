---
title: 创建变量值文件 (AccessToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/17/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 808595c3-8ef1-40bd-a93e-5cf237950e08
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 00144c51e60b72fe043443d2a9c8d1d51a6cb8da
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63138829"
---
# <a name="creating-variable-value-files-accesstosql"></a>创建变量值文件 (AccessToSQL)
变量值文件是 XML 文件包含的命令 （如源或目标服务器名称） 的服务器迁移而频繁更改的参数值。 大量的数据库迁移发生时，创建和使用主脚本文件中引用多个变量文件用于存储每个源服务器的值 **-v**在命令行开关。 此行为有助于维护几个脚本文件中的静态值，与多个变量文件中的变量值。  
  
> [!NOTE]  
> -  变量名称是作为前缀和后缀，以 $ （美元） 符号。 如果变量未分配的变量值文件中的值，在脚本文件的分析过程将会出错，导致拖延症控制台执行过程。  
> -  转义符**$** 是**$$**。 如果参数的变量或静态值的值包含**$** （美元） 符号，然后**$$** 必须指定将其视为字符而不是一个变量。  
> -  出于可维护性目的，可以在声明变量`'variable-group'`用户定义的变量的逻辑分隔的元素。  此元素的使用情况不是必需的。  
  
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
用户可以轻松地验证他/她变量值文件是否符合架构定义文件**ConsoleScriptVariablesSchema.xsd**架构文件夹中可用。  
  
## <a name="next-step"></a>下一步  
在操作控制台中的下一步是[创建服务器连接文件&#40;AccessToSQL&#41;](../../ssma/access/creating-the-server-connection-files-accesstosql.md)  
  
## <a name="see-also"></a>另请参阅  
[创建服务器连接文件 （访问）](https://msdn.microsoft.com/829153be-aa8e-4162-87e8-69882feecf19)  
  
