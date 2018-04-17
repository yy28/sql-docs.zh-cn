---
title: 连接到 Windows Azure SQL 数据库使用 SQL Server Native Client |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: native-client|applications
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 0dc20bb6-b142-4259-b87b-427d2ba798af
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 8145383913d7de07a1a6baf352eea1c3b9ede630
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="connecting-to-a-windows-azure-sql-database-using-sql-server-native-client"></a>使用 SQL Server Native Client 连接到 Windows Azure SQL Database
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  有关示例，演示如何连接到[!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)]使用[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本机客户端，请参阅[开发： 操作指南主题 （Windows Azure SQL 数据库）](http://msdn.microsoft.com/library/ee621787.aspx)。  
  
## <a name="known-issues-when-connecting-to-a-sql-database"></a>连接到 SQL Database 时的已知问题  
 以下是使用 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] Native Client 连接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 时的一些已知问题：  
  
-   与建立的连接**SQLBrowseConnect**可能会被拒绝**SQLBrowseConnect**阶段中使用。  例如，如果在第一次调用中发送驱动程序名称，在第二次调用中发送服务器和凭据（用户名和密码），建立连接，然后在第三次调用中发送数据库名称和语言。  第三次调用将导致 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 发出 USE 语句来更改数据库。 但是，在 [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] 中不支持 USE 语句，因此生成以下错误：  
  
    ```  
    [Microsoft][SQL Server Native Client 11.0][SQL Server]USE statement is not supported to switch between databases. Use a new connection to connect to a different Database.  
    ```  
  
## <a name="see-also"></a>另请参阅  
 [使用 SQL Server Native Client 生成应用程序](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
