---
title: 创建变量值文件 (SybaseToSQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Sybase Console,Creating Variable Value Files
- Sybase Console,Variable Value File Validation
ms.assetid: 395be464-4b19-44f7-91e5-b8876d6743dc
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 7afced10f0be71310edc4b42ea0158ca996f3aa3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63069662"
---
# <a name="creating-variable-value-files-sybasetosql"></a>创建变量值文件 (SybaseToSQL)
变量值文件是 XML 文件包含的频繁更改从一台服务器迁移到另一个如源或目标服务器名称的命令的参数值。 大量的数据库迁移发生时，将创建并使用主脚本文件中引用多个变量文件用于存储每个源服务器的值 **-v**在命令行开关。 这有助于维护几个脚本文件中的静态值，与多个变量文件中的变量值。  
  
> [!NOTE]  
> 1.  变量名称是作为前缀和后缀，以 $ （美元） 符号。 如果变量未分配的变量值文件中的值，将导致停止控制台执行过程的脚本文件的分析过程中遇到错误。  
> 2.  转义符 **$** 是 **$$** 。 如果参数的变量或静态值的值将包含 **$** （美元） 符号，然后 **$$** 必须指定将其视为字符而不是一个变量。  
> 3.  出于可维护性目的，可以在声明变量`'variable-group'`元素的逻辑分隔的用户定义的变量。  此元素的使用情况不是必需的。  
  
**示例：**  
  
**示例 1:**  
  
```xml  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="ProjectSpecs">  
  
    <variable name="$project_folder$" value="<project-folder>"/>  
  
    <variable name="$project_name$" value="<project-name>"/>  
  
    <variable name="$project_overwrite$" value="<true/false>"/>  
  
    <variable name="$project_type$" value="<project-type>"/>  
  
  </variable-group>  
  
</variables>  
```  
**示例 2:**  
  
```xml  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="SQLServerParams">  
  
    <variable-group name="SqlServerConnectionParams">  
  
      <variable name="$TargetUserName$" value="<user-name>"/>  
  
      <variable name="$TargetServerName$" value="<server-name>"/>  
  
      <variable name="$TargetDB$" value="<database-name>"/>  
  
      <variable name="$TargetPassword$" value="<password>"/>  
  
      <variable name="$TrustedConnection$" value="<true/false>"/>  
  
    </variable-group>  
  
    <variable-group name="SqlServerObjectParams">  
  
      <variable name="$ObjectName1$" value="<object-name>"/>  
  
      <variable name="$ObjectName2$" value="<object-name>"/>  
  
    </variable-group>  
  
  </variable-group>  
  
</variables>  
```  
  
## <a name="variable-value-file-validation"></a>变量值文件验证  
用户可以轻松地验证他/她变量值文件是否符合架构定义文件**ConsoleScriptVariablesSchema.xsd**架构文件夹中可用。  
  
## <a name="next-step"></a>下一步  
在操作控制台中的下一步是[创建服务器连接文件&#40;SybaseToSQL&#41;](../../ssma/sybase/creating-the-server-connection-files-sybasetosql.md)  
  
## <a name="see-also"></a>请参阅  
[创建服务器文件 (Sybase)](https://msdn.microsoft.com/35ef396f-9f98-429d-9fc5-4f413d08fb37)  
  
