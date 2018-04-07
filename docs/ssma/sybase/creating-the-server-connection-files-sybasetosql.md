---
title: 创建服务器连接文件 (SybaseToSQL) |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Sybase Console,Creating Server Connection Files
- Sybase Console,Server Connection File Validation
ms.assetid: 35ef396f-9f98-429d-9fc5-4f413d08fb37
caps.latest.revision: 14
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a4466dff337914b4598442ab0377a9d3457aad8b
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="creating-the-server-connection-files-sybasetosql"></a>创建服务器连接文件 (SybaseToSQL)
脚本文件的服务器部分中，也可在单独的服务器连接文件，可以指定服务器信息。 服务器连接文件的命令行参数， `-c <serverconnectionfile>`。 如果脚本文件和服务器连接文件中存在相同的服务器 id，则被视为脚本文件中的服务器定义。  
  
**示例：**  
  
```  
1.<!--Sample of server connection file commands -->  
  
<sybase name="<source-server-unique-name>">  
  
  <standard-mode>  
  
    <provider value="Ole DB Provider"/>  
  
    <server-name value="<server-name>"/>  
  
    <server-port value="<port>"/>  
  
    <user-id value="<password>"/>  
  
  </standard-mode>  
  
</sybase>  
```  
  
```xml  
<!--Connection to SQL Server-->  
  
<sql-server name="<target-server-unique-name>">  
  
  <sql-server-authentication>  
  
    <database value="<database-name>"/>  
  
    <server value="<server-name>"/>  
  
    <user-id value="<user-name>"/>  
  
    <password value="<password>"/>  
  
    <encrypt value="<true/false>"/>  
  
    <trust-server-certificate value="<true/false>"/>  
  
  </sql-server-authentication >  
  
</sql-server>  
```  
  
```  
2.<!—Sample of server connection file commands-->  
<sybase name="<source-server-unique-name>">  
  
  <advanced-mode>  
  
    <connection-string value="User ID=<user-name>;Password=<password>;Provider=ASEOLEDB.1;Server=<server-name>;Port=<port>;OLE DB Services = -2;"/>  
  
  </advanced-mode >  
  
</sybase>  
```  
  
```xml  
<!--Connection to SQL Server-->  
  
<sql-server name="<target-server-unique-name>">  
  
  <sql-server-authentication >  
  
    <database value="<database-name>"/>  
  
    <server value="<server-name>"/>  
  
    <user-id value="<user-name>"/>  
  
    <password value="<password>"/>  
  
  </sql-server-authentication >  
  
</sql-server>  
```  
  
## <a name="server-connection-file-validation"></a>服务器连接文件验证  
用户可以轻松地验证他/她服务器连接文件的架构定义文件和**S2SSConsoleScriptServersSchema.xsd**架构文件夹中可用。  
  
## <a name="next-step"></a>下一步  
操作控制台的下一步是[执行 SSMA 控制台&#40;SybaseToSQL&#41;](../../ssma/sybase/executing-the-ssma-console-sybasetosql.md)  
  
## <a name="see-also"></a>另请参阅  
[执行 SSMA 控制台](http://msdn.microsoft.com/en-us/ea8950b7-fabc-4aa4-89f8-9573a2617d70)  
  
