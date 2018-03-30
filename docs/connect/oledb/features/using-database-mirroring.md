---
title: 使用数据库镜像 |Microsoft 文档
description: 使用数据库镜像与 OLE DB 驱动程序的 SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- database mirroring [SQL Server], interoperability
- OLE DB Driver for SQL Server, database mirroring
- data access [OLE DB Driver for SQL Server], database mirroring
- database mirroring [SQL Server], connecting clients to
- MSOLEDBSQL, database mirroring
- OLE DB Driver for SQL Server, database mirroring
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b4b8b08f86e4aab588accd58ada1da44179b4cee
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2018
---
# <a name="using-database-mirroring"></a>使用数据库镜像
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]使用[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]相反。  
  
 在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 中引入的数据库镜像是一种提高数据库可用性和改善数据冗余性的解决方案。 OLE DB 驱动程序的 SQL Server 提供隐式支持数据库镜像，以便开发人员不需要编写任何代码或配置数据库后执行任何其他操作。  
  
 数据库镜像，基于每个数据库实现，保留一份[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]备用服务器上的生产数据库。 该服务器根据数据库镜像会话的配置和状态，充当热备用或温备用服务器。 热备用服务器支持快速故障转移且不会丢失已提交事务，温备用服务器支持强制服务（可能丢失数据）。  
  
 生产数据库就称为*主体数据库*，和的备用副本称为*镜像数据库*。 主体数据库和镜像数据库必须驻留在单独的实例上[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]（服务器实例），并且它们应尽可能驻留在单独的计算机上。  
  
 调用的生产服务器实例*主体服务器*，与调用的备用服务器实例进行通信*镜像服务器*。 主体和镜像服务器充当中数据库镜像伙伴*会话*。 如果主体服务器出现故障，镜像服务器可以使其数据库成为主体数据库通过一个称为过程*故障转移*。 例如，Partner_A 和 Partner_B 是两个伙伴服务器，主体数据库最初位于作为主体服务器的 Partner_A 中，镜像数据库位于作为镜像服务器的 Partner_B 中。 如果 Partner_A 脱机，Partner_B 上的数据库可以进行故障转移，成为当前的主体数据库。 当 Partner_A 重新加入镜像会话时，该服务器变为镜像服务器，并且其数据库变为镜像数据库。  
  
 备用数据库镜像配置提供不同级别的性能和数据安全，并支持不同形式的故障转移。 有关详细信息，请参阅[数据库镜像 (SQL Server)](../../../database-engine/database-mirroring/database-mirroring-sql-server.md)。  
  
 指定镜像数据库名称时可以使用别名。  
  
> [!NOTE]  
>  有关初始连接尝试和将尝试重新连接到镜像数据库的信息，请参阅[将客户端连接到数据库镜像会话&#40;SQL Server&#41;](../../../database-engine/database-mirroring/connect-clients-to-a-database-mirroring-session-sql-server.md)。  
  
## <a name="programming-considerations"></a>编程时的注意事项  
 当主体数据库服务器失败时，客户端应用程序则接收错误以响应 API 调用，这指示与数据库之间的连接已丢失。 发生此种情况时，对数据库执行的任何未提交的更改将丢失，并回滚当前事务。 如果发生这种情况，应用程序应关闭连接（或释放数据源对象），然后再重新打开它。 连接将以透明方式重新定向到镜像数据库，该数据库现在充当主体服务器。  
  
 建立连接时，主体服务器将其故障转移伙伴的标识发送到客户端，以便在发生故障转移时使用。 当应用程序在主体服务器失败后尝试建立连接时，客户端不知道故障转移伙伴的标识。 为使客户端能够处理这种情况，初始化属性和关联的连接字符串关键字允许客户端自己指定故障转移伙伴的标识。 客户端属性仅在此种情况下使用；如果主体服务器可用，则不使用此属性。 如果客户端提供的故障转移伙伴服务器未引用充当故障转移伙伴的服务器，该服务器将拒绝连接。 若要使应用程序适应配置更改，可以通过在建立连接后检测该属性来确定实际故障转移伙伴的标识。 如果首次尝试建立连接失败，则应考虑缓存伙伴信息，以更新连接字符串或设计重试策略。  
  
> [!NOTE]  
>  如果希望在 DSN、连接字符串或连接属性/特性中使用此功能，必须显式指定连接要使用的数据库。 如果不执行此操作，OLE DB 驱动程序的 SQL Server 不会尝试故障转移到合作伙伴数据库。  
>   
>  镜像是面向数据库的功能。 使用多个数据库的应用程序可能无法利用此功能。  
>   
>  此外，服务器名称不区分大小写，而数据库名称区分大小写。 因此，应确保在 DSN 和连接字符串中使用相同的大小写。  
  
## <a name="ole-db-driver-for-sql-server"></a>用于 SQL Server 的 OLE DB 驱动程序  
 SQL Server 的 OLE DB 驱动程序支持数据库镜像通过连接和连接字符串属性。 SSPROP_INIT_FAILOVERPARTNER 属性已添加到 dbpropset_sqlserverdbinit 限属性集，与**FailoverPartner**关键字是 DBPROP_INIT_PROVIDERSTRING 的新连接字符串属性。 有关详细信息，请参阅[OLE DB 驱动程序的 SQL Server 连接字符串关键字](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)。  
  
 只要加载提供程序后，即直到维护故障转移缓存**CoUninitialize**调用或只要应用程序具有对某个对象由 OLE DB 驱动程序适用于 SQL Server 管理，如数据源对象的引用.  
  
 有关 OLE DB 驱动程序的数据库镜像的 SQL Server 支持的详细信息，请参阅[初始化和授权属性](../../oledb/ole-db-data-source-objects/initialization-and-authorization-properties.md)。  
 
  
## <a name="see-also"></a>另请参阅  
 [用于 SQL Server 功能的 OLE DB 驱动程序](../../oledb/features/oledb-driver-for-sql-server-features.md)   
 [将客户端连接到数据库镜像会话 (SQL Server)](../../../database-engine/database-mirroring/connect-clients-to-a-database-mirroring-session-sql-server.md)   
 [数据库镜像 (SQL Server)](../../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  
