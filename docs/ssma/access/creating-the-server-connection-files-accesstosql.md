---
title: 创建服务器连接文件 (AccessToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/17/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 829153be-aa8e-4162-87e8-69882feecf19
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: f083b38d64927ded898366434def4505cd3f67c7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47672655"
---
# <a name="creating-the-server-connection-files-accesstosql"></a>创建服务器连接文件 (AccessToSQL)
服务器信息可以是指定在脚本文件的服务器部分。 此外可以在单独的服务器连接文件中指定服务器信息。 服务器连接文件的命令行参数是`-c <serverconnectionfile>`。 如果脚本和服务器连接文件中存在相同的服务器 id，则被视为脚本文件中的服务器定义。  
  
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
用户可以轻松地验证他/她服务器连接文件和架构定义文件**A2SSConsoleScriptServersSchema.xsd**架构文件夹中可用。  
  
## <a name="next-step"></a>下一步  
在操作控制台中的下一步是[执行 SSMA 控制台&#40;AccessToSQL&#41;](../../ssma/access/executing-the-ssma-console-accesstosql.md)  
  
## <a name="see-also"></a>另请参阅  
[执行 SSMA 控制台 （访问）](http://msdn.microsoft.com/aa1bf665-8dc0-4259-b36f-46ae67197a43)  
  
