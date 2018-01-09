---
title: "使用数据库镜像 |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client|features
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- database mirroring [SQL Server], interoperability
- SQL Server Native Client, database mirroring
- data access [SQL Server Native Client], database mirroring
- database mirroring [SQL Server], connecting clients to
- SQLNCLI, database mirroring
- SQL Server Native Client ODBC driver, database mirroring
- SQL Server Native Client OLE DB provider, database mirroring
ms.assetid: 71b15712-7972-4465-9274-e0ddc271eedc
caps.latest.revision: "55"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b57f77a051e2490238d88f8bc336ce34fb0e380b
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="using-database-mirroring"></a>使用数据库镜像
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)] 改为使用 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]。  
  
 在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中引入的数据库镜像是一种提高数据库可用性和改善数据冗余性的解决方案。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]本机客户端提供隐式支持数据库镜像，以便开发人员不需要编写任何代码或配置数据库后执行任何其他操作。  
  
 数据库镜像，基于每个数据库实现，保留一份[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]备用服务器上的生产数据库。 该服务器根据数据库镜像会话的配置和状态，充当热备用或温备用服务器。 热备用服务器支持快速故障转移且不会丢失已提交事务，温备用服务器支持强制服务（可能丢失数据）。  
  
 生产数据库就称为*主体数据库*，和的备用副本称为*镜像数据库*。 主体数据库和镜像数据库必须驻留在单独的实例上[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]（服务器实例），并且它们应尽可能驻留在单独的计算机上。  
  
 调用的生产服务器实例*主体服务器*，与调用的备用服务器实例进行通信*镜像服务器*。 主体和镜像服务器充当中数据库镜像伙伴*会话*。 如果主体服务器出现故障，镜像服务器可以使其数据库成为主体数据库通过一个称为过程*故障转移*。 例如，Partner_A 和 Partner_B 是两个伙伴服务器，主体数据库最初位于作为主体服务器的 Partner_A 中，镜像数据库位于作为镜像服务器的 Partner_B 中。 如果 Partner_A 脱机，Partner_B 上的数据库可以进行故障转移，成为当前的主体数据库。 当 Partner_A 重新加入镜像会话时，该服务器变为镜像服务器，并且其数据库变为镜像数据库。  
  
 备用数据库镜像配置提供不同级别的性能和数据安全，并支持不同形式的故障转移。 有关详细信息，请参阅[数据库镜像 (SQL Server)](../../../database-engine/database-mirroring/database-mirroring-sql-server.md)。  
  
 指定镜像数据库名称时可以使用别名。  
  
> [!NOTE]  
>  有关初始连接尝试和将尝试重新连接到镜像数据库的信息，请参阅[将客户端连接到数据库镜像会话 &#40;SQL server&#41;](../../../database-engine/database-mirroring/connect-clients-to-a-database-mirroring-session-sql-server.md).  
  
## <a name="programming-considerations"></a>编程时的注意事项  
 当主体数据库服务器失败时，客户端应用程序则接收错误以响应 API 调用，这指示与数据库之间的连接已丢失。 发生此种情况时，对数据库执行的任何未提交的更改将丢失，并回滚当前事务。 如果发生这种情况，应用程序应关闭连接（或释放数据源对象），然后再重新打开它。 连接将以透明方式重新定向到镜像数据库，该数据库现在充当主体服务器。  
  
 建立连接时，主体服务器将其故障转移伙伴的标识发送到客户端，以便在发生故障转移时使用。 当应用程序在主体服务器失败后尝试建立连接时，客户端不知道故障转移伙伴的标识。 为使客户端能够处理这种情况，初始化属性和关联的连接字符串关键字允许客户端自己指定故障转移伙伴的标识。 客户端属性仅在此种情况下使用；如果主体服务器可用，则不使用此属性。 如果客户端提供的故障转移伙伴服务器未引用充当故障转移伙伴的服务器，该服务器将拒绝连接。 若要使应用程序适应配置更改，可以通过在建立连接后检测该属性来确定实际故障转移伙伴的标识。 如果首次尝试建立连接失败，则应考虑缓存伙伴信息，以更新连接字符串或设计重试策略。  
  
> [!NOTE]  
>  如果希望在 DSN、连接字符串或连接属性/特性中使用此功能，必须显式指定连接要使用的数据库。 否则，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 将不会尝试故障转移到伙伴数据库。  
>   
>  镜像是面向数据库的功能。 使用多个数据库的应用程序可能无法利用此功能。  
>   
>  此外，服务器名称不区分大小写，而数据库名称区分大小写。 因此，应确保在 DSN 和连接字符串中使用相同的大小写。  
  
## <a name="sql-server-native-client-ole-db-provider"></a>SQL Server Native Client OLE DB 访问接口  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序支持数据库镜像通过连接和连接字符串属性。 SSPROP_INIT_FAILOVERPARTNER 属性已添加到 dbpropset_sqlserverdbinit 限属性集，与**FailoverPartner**关键字是 DBPROP_INIT_PROVIDERSTRING 的新连接字符串属性。 有关详细信息，请参阅[Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)。  
  
 只要加载提供程序后，即直到维护故障转移缓存**CoUninitialize**是只要应用程序具有由某个对象的引用或调用[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]如 Native Client OLE DB 提供程序数据源对象。  
  
 有关详细信息[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序支持数据库镜像，请参阅[初始化和授权属性](../../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md)。  
  
## <a name="sql-server-native-client-odbc-driver"></a>SQL Server Native Client ODBC 驱动程序  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序支持数据库镜像通过连接和连接字符串属性。 具体而言，SQL_COPT_SS_FAILOVER_PARTNER 属性已添加用于[SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)和[SQLGetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md)函数; 与**Failover_Partner**关键字已添加的新的连接字符串属性。  
  
 只要应用程序至少分配有一个环境句柄，故障转移缓存就会一直保留。 相反，当释放最后一个环境句柄时，将丢失故障转移缓存。  
  
> [!NOTE]  
>  ODBC 驱动程序管理器已得以改进，能够支持指定故障转移服务器名称。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Native Client 功能](../../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [将客户端连接到数据库镜像会话 (SQL Server)](../../../database-engine/database-mirroring/connect-clients-to-a-database-mirroring-session-sql-server.md)   
 [数据库镜像 (SQL Server)](../../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  
