---
title: "登录到 SQL Server 实例（命令提示符）| Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- logins [SQL Server], named instance of SQL Server
- log ins [SQL Server]
- logins [SQL Server], default instance of SQL Server
- command prompt [SQL Server], logins
- logging in [SQL Server]
ms.assetid: f67c11e3-c519-40c9-82c1-07efa9d9985e
caps.latest.revision: "26"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: f5899510b24205d4ebc82dc5779505c522b340d6
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="log-in-to-an-instance-of-sql-server-command-prompt"></a>登录到 SQL Server 实例（命令提示符）
  本主题介绍如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]sqlcmd **实用工具测试与** 实例的连接。  
  
##  <a name="SSMSProcedure"></a>  
  
#### <a name="to-log-in-to-the-default-instance-of-sql-server"></a>登录到 SQL Server 的默认实例  
  
1.  从命令提示符输入以下命令，使用 Windows 身份验证进行连接：  
  
    ```  
    sqlcmd [ /E ] [ /S servername ]  
  
    ```  
  
#### <a name="to-log-in-to-a-named-instance-of-sql-server"></a>登录到 SQL Server 的命名实例  
  
1.  从命令提示符输入以下命令，使用 Windows 身份验证进行连接：  
  
    ```  
    sqlcmd [ /E ] /S servername\instancename  
  
    ```  
  
## <a name="see-also"></a>另请参阅  
 [sqlcmd 实用工具](../../tools/sqlcmd-utility.md)   
 [osql 实用工具](../../tools/osql-utility.md)  
  
  
