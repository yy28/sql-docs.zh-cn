---
title: 创建服务器连接文件（MySQLToSQL） |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Server connection file validation
- Server connection files
ms.assetid: df0e970c-da0b-4118-b359-c9dcbbad16d6
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 1df2c474afa5e062dfa22cf05af6b0edf036f768
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68103038"
---
# <a name="creating-the-server-connection-files-mysqltosql"></a>创建服务器连接文件 (MySQLToSQL)
服务器信息可以在脚本文件的 "服务器" 部分中指定，也可以在单独的服务器连接文件中指定。 服务器连接文件的命令行参数为， `-c <serverconnectionfile>`。 如果脚本文件和服务器连接文件中同时存在相同的服务器 id，则考虑脚本文件中的服务器定义。  
  
**示例：**  
  
```xml  
<!--Sample of server connection file commands -->  
  
<mysql name ="<source-server-unique-name>">  
  
   <standard-mode>  
  
      <server value ="<server-name>"/>  
  
      <user-id value ="<user-name>"/>  
  
      <password value ="<password>"/>  
  
      <port value ="<port>"/>  
  
   </standard-mode>  
  
</mysql>  
```  
  
```xml  
<!--Connection to SQL Server-->  
  
<sql-server name="<target-server-unique-name>">  
  
   <sql-server-authentication>  
  
      <server value="<server-name>"/>  
  
      <database value="<database-name>"/>  
  
      <user-id value="<user-name>"/>  
  
      <password value="<password>"/>  
  
      <encrypt value="<true/false>"/>  
  
      <trust-server-certificate value="<true/false>"/>  
  
   </sql-server-authentication>  
  
</sql-server>  
```  
  
```xml  
<!--Connection to SQL Azure-->  
  
<sql-azure name="<target-server-unique-name>">  
  
   <server value="<server-name>"/>  
  
   <database value="<database-name>"/>  
  
   <user-id value="<user-name>"/>  
  
   <password value="<password>"/>  
  
</sql-azure>  
```  
  
## <a name="server-connection-file-validation"></a>服务器连接文件验证  
用户可以根据 "架构" 文件夹中提供的架构定义文件 " **2ssconsolescriptserversschema"** 来轻松验证其服务器连接文件。  
  
## <a name="next-step"></a>下一步  
操作控制台的下一步是[执行 SSMA 控制台 &#40;MySQLToSQL&#41;](../../ssma/mysql/executing-the-ssma-console-mysqltosql.md)  
  
## <a name="see-also"></a>另请参阅  
[执行 SSMA 控制台（MySQL）](https://msdn.microsoft.com/e3e9f7e4-0619-4861-a202-3d5d39953b26)  
  
