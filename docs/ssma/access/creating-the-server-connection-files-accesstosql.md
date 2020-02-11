---
title: 创建服务器连接文件（AccessToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/17/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 829153be-aa8e-4162-87e8-69882feecf19
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 03d622c50a8760bbf1767bc8a4f79e215773695f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68006603"
---
# <a name="creating-the-server-connection-files-accesstosql"></a>创建服务器连接文件（AccessToSQL）
可以在脚本文件的 "服务器" 部分中指定服务器信息。 还可以在单独的服务器连接文件中指定服务器信息。 服务器连接文件的命令行参数为`-c <serverconnectionfile>`。 如果脚本和服务器连接文件中同时存在相同的服务器 id，则考虑脚本文件中的服务器定义。  
  
```xml  
<!--Sample of server connection file commands -->  
<!--Connection to SQL Server-->  
  
<sql-server name="target_3">  
  
  <sql-server-authentication>  
  
    <server value="$TargetServerName$"/>  
  
    <database value="$TargetDB$"/>  
  
    <user-id value="$TargetUserName$"/>  
  
    <password value="$TargetPassword$"/>  
  
    <encrypt value="true"/>  
  
    <trust-server-certificate value="true"/>  
  
  </sql-server-authentication>  
  
</sql-server>  
```  
  
```xml  
<!--Connection to SQL Azure-->  
  
<sql-azure name="target_azure">  
  
  <server value="$TargetAzureServerName$"/>  
  
  <database value="$TargetAzureDB$"/>  
  
  <user-id value="$TargetAzureUserName$"/>  
  
  <password value="$TargetAzurePassword$"/>  
  
</sql-azure>  
```  
  
## <a name="server-connection-file-validation"></a>服务器连接文件验证  
用户可以根据 "架构" 文件夹中提供的架构定义文件 **"A2SSConsoleScriptServersSchema"** 轻松地验证其服务器连接文件。  
  
## <a name="next-step"></a>后续步骤  
操作控制台的下一步是[执行 SSMA 控制台 &#40;AccessToSQL&#41;](../../ssma/access/executing-the-ssma-console-accesstosql.md)  
  
## <a name="see-also"></a>另请参阅  
[执行 SSMA 控制台（Access）](https://msdn.microsoft.com/aa1bf665-8dc0-4259-b36f-46ae67197a43)  
  
