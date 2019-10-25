---
title: SQL Server 中的数据库镜像
description: 介绍数据库镜像功能。
ms.date: 09/30/2019
dev_langs:
- csharp
ms.assetid: 89befaff-bb46-4290-8382-e67cdb0e3de9
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 1c78f52f376ff6c333b952b8d013e17eefce45ea
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452273"
---
# <a name="database-mirroring-in-sql-server"></a>SQL Server 中的数据库镜像

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[下载 ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

通过 SQL Server 中的数据库镜像，可以在备用服务器上保留 SQL Server 数据库的副本（即镜像）。 镜像确保数据的两个单独副本始终存在，从而提供高可用性和完整的数据冗余。 适用于 SQL Server 的 Microsoft SqlClient 提供程序对数据库镜像提供隐式支持，因此在为 SQL Server 数据库配置了镜像之后，开发人员不需要采取任何措施或编写任何代码。 此外，<xref:Microsoft.Data.SqlClient.SqlConnection> 对象支持显式连接模式，该模式允许在 <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A> 中提供故障转移伙伴服务器的名称。  
  
对于针对为镜像配置的数据库的 <xref:Microsoft.Data.SqlClient.SqlConnection> 对象，会发生以下简化的事件序列：  
  
1. 客户端应用程序成功连接到主体数据库，服务器发送回伙伴服务器的名称，然后在客户端上缓存该服务器。  
  
2. 如果包含主体数据库的服务器发生故障或连接中断，则连接和事务状态将丢失。 客户端应用程序尝试重新建立与主体数据库的连接，但失败。  
  
3. 然后，客户端应用程序以透明方式尝试与伙伴服务器上的镜像数据库建立连接。 如果成功，连接将重定向到镜像数据库，后者随后会成为新的主体数据库。  
  
## <a name="specifying-the-failover-partner-in-the-connection-string"></a>在连接字符串中指定故障转移伙伴  
如果在连接字符串中提供故障转移伙伴服务器的名称，则当客户端应用程序首次连接时，主体数据库不可用时，客户端将以透明方式尝试连接到故障转移伙伴。  
  
```csharp
";Failover Partner=PartnerServerName"  
```  
  
如果省略故障转移伙伴服务器的名称，并且在客户端应用程序首次连接时，主体数据库不可用，则会引发 <xref:Microsoft.Data.SqlClient.SqlException>。  
  
如果成功打开 <xref:Microsoft.Data.SqlClient.SqlConnection>，则服务器将返回故障转移伙伴名称，并取代在连接字符串中提供的任何值。  
  
> [!NOTE]
>  您必须在数据库镜像方案的连接字符串中显式指定初始目录或数据库名称。 如果客户端接收没有显式指定初始编录或数据库的连接的故障转移信息，故障转移信息不会缓存，应用程序也不会在主体服务器失败时尝试进行故障转移。 如果连接字符串的故障转移伙伴值为，但没有用于初始目录或数据库的值，则会引发 `InvalidArgumentException`。  
  
## <a name="retrieving-the-current-server-name"></a>检索当前服务器名称  
发生故障转移时，可以使用 <xref:Microsoft.Data.SqlClient.SqlConnection> 对象的 <xref:Microsoft.Data.SqlClient.SqlConnection.DataSource%2A> 属性，检索当前连接实际连接到的服务器的名称。 下面的代码段检索活动服务器的名称，前提是该连接变量引用了一个打开的 <xref:Microsoft.Data.SqlClient.SqlConnection>。  
  
发生故障转移事件并将连接切换到镜像服务器时，会更新**DataSource**属性以反映镜像名称。  
  
```csharp  
string activeServer = connection.DataSource;  
```  
  
## <a name="sqlclient-mirroring-behavior"></a>SqlClient 镜像行为  
客户端始终尝试连接到当前的主体服务器。 如果失败，它将尝试故障转移伙伴。 如果镜像数据库已切换到伙伴服务器上的主体角色，则连接将成功，并且新的主体镜像映射将发送到客户端，并在调用 <xref:System.AppDomain> 的生存期内缓存。 映射不会存储在永久存储空间中，也无法供其他 AppDomain 或进程中的后续连接使用。 但是，可以供相同 AppDomain 中的后续连接使用。 注意，在相同或不同的计算机上运行的其他 AppDomain 或进程总是拥有自己的连接池，这些连接不会重置。 在这种情况下，如果主数据库关闭，每个进程或 AppDomain 将失败，池将被自动清除。  
  
> [!NOTE]
>  服务器上的镜像支持是基于每个数据库配置的。 如果对不包含在主体/镜像集中的其他数据库执行数据操作操作，则可以通过使用多部分名称或更改当前数据库，对这些其他数据库的更改在发生故障时不会传播。 在未镜像的数据库中修改数据时，不会生成错误。 开发人员必须评估此类操作的可能影响。  
  
## <a name="next-steps"></a>后续步骤
### <a name="database-mirroring-resources"></a>数据库镜像资源  
有关配置、部署和管理镜像的概念性文档及信息，请参阅 SQL Server 文档中的下列资源。  
  
|资源|描述|  
|--------------|-----------------|  
|[数据库镜像](../../../database-engine/database-mirroring/database-mirroring-sql-server.md)|介绍在 SQL Server 中设置和配置镜像的方法。|  
