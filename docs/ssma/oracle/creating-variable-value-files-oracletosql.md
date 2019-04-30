---
title: 创建变量值文件 (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Variable Value File Creation
- Variable Value File, Variable Value File Validation
ms.assetid: f583d81a-8e34-41b1-8100-ee3a6a82213b
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 067781fd998c9e7763fe3a9f2befacab59687250
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63287170"
---
# <a name="creating-variable-value-files-oracletosql"></a>创建变量值文件 (OracleToSQL)
变量值文件是 XML 文件包含的频繁更改从一台服务器迁移到另一个如源或目标服务器名称的命令的参数值。 大量的数据库迁移发生时，将创建并使用主脚本文件中引用多个变量文件用于存储每个源服务器的值 **-v**在命令行开关。 这有助于维护几个脚本文件中的静态值，与多个变量文件中的变量值。  
  
> [!NOTE]  
> 1.  变量名称是作为前缀和后缀，以 $ （美元） 符号。 如果变量未分配的变量值文件中的值，将导致停止控制台执行过程的脚本文件的分析过程中遇到错误。  
> 2.  转义符**$** 是**$$**。 如果参数的变量或静态值的值将包含**$** （美元） 符号，然后**$$** 必须指定将其视为字符而不是一个变量。  
> 3.  出于可维护性目的，可以在声明变量`'variable-group'`元素的逻辑分隔的用户定义的变量。  此元素的使用情况不是必需的。  
  
**示例：**  
  
**示例 1:**  
  
```  
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
  
```  
<!--Sample of variable value file commands-->  
  
<variables>  
  
  <variable-group name="SQLServerParams">  
  
    <variable-group name="SqlServerConnectionParams">  
  
      <variable name="$TargetServerName$" value="<server-name>"/>  
  
      <variable name="$TargetDB$" value="<database-name>"/>  
  
      <variable name="$TargetUserName$" value="<user-name>"/>  
  
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
  
## <a name="next-step"></a>下一步  
在操作控制台中的下一步是[创建服务器连接文件&#40;OracleToSQL&#41;](../../ssma/oracle/creating-the-server-connection-files-oracletosql.md)  
  
## <a name="see-also"></a>请参阅  
[创建服务器文件 (Oracle)](https://msdn.microsoft.com/002f129e-0868-48ad-a4b4-c68b5007e12e)  
  
