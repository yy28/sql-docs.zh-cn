---
title: 登录到 SQL Server 实例（命令提示符）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- logins [SQL Server], named instance of SQL Server
- log ins [SQL Server]
- logins [SQL Server], default instance of SQL Server
- command prompt [SQL Server], logins
- logging in [SQL Server]
ms.assetid: f67c11e3-c519-40c9-82c1-07efa9d9985e
caps.latest.revision: 23
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 266da633926e1d79236fb0a9f6045b45790c8e49
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36129741"
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
  
## <a name="see-also"></a>请参阅  
 [sqlcmd 实用工具](../../tools/sqlcmd-utility.md)   
 [osql 实用工具](../../tools/osql-utility.md)  
  
  