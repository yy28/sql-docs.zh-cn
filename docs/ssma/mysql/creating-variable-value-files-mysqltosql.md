---
title: "创建变量值文件 (MySQLToSQL) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-mysql
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Creating variable value files
- variable value file validation
ms.assetid: 1dc56a7b-8e3a-4576-ad4f-47050bf7e28a
caps.latest.revision: "16"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1cd159682512255ab253630ac762fbeac104ab14
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="creating-variable-value-files-mysqltosql"></a>创建变量值文件 (MySQLToSQL)
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
  
    <variable name="$project_folder$" value="<folder-name>"/>  
  
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
  
      <variable name="$TargetUserName$ value="<user-name>"/>  
  
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
用户可以轻松地验证他/她变量值文件是否符合的架构定义文件**ConsoleScriptVariablesSchema.xsd**架构文件夹中可用。  
  
## <a name="next-step"></a>下一步  
操作控制台的下一步是[创建服务器连接文件 &#40;MySQLToSQL &#41;](../../ssma/mysql/creating-the-server-connection-files-mysqltosql.md)  
  
## <a name="see-also"></a>另请参阅  
[创建服务器连接文件 (MySQL)](http://msdn.microsoft.com/en-us/df0e970c-da0b-4118-b359-c9dcbbad16d6)  
  
