---
title: 用于高可用性、 灾难恢复的 SQL Server 支持的 OLE DB 驱动程序 |Microsoft 文档
description: OLE DB 驱动程序的 SQL Server 支持的高可用性、 灾难恢复
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 02f6c8da18d94c243ea9c3c07717af5b9750b066
ms.sourcegitcommit: 354ed9c8fac7014adb0d752518a91d8c86cdce81
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/14/2018
ms.locfileid: "35612162"
---
# <a name="ole-db-driver-for-sql-server-support-for-high-availability-disaster-recovery"></a>用于高可用性、 灾难恢复的 SQL Server 支持的 OLE DB 驱动程序
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  本文介绍 SQL Server 支持 OLE DB 驱动程序 (在中添加[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]) 为[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]。 有关 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 的详细信息，请参阅[可用性组侦听器、客户端连接和应用程序故障转移 (SQL Server)](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)、[创建和配置可用性组 (SQL Server)](../../../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md)、[故障转移群集和 AlwaysOn 可用性组 (SQL Server)](../../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md) 和[活动次要副本：可读次要副本（AlwaysOn 可用性组）](../../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)。  
  
 您可以在连接字符串中指定给定可用性组的可用性组侦听器。 如果 SQL Server 应用程序用于 OLE DB 驱动程序连接到故障转移可用性组中的数据库，原始连接已断开，并且该应用程序必须打开新的连接在故障转移后继续工作。  
  
 如果你没有连接到可用性组侦听器，并且如果多个 IP 地址关联一个主机名，OLE DB 驱动程序的 SQL Server 将按顺序循环访问与 DNS 条目关联的所有 IP 地址。 如果 DNS 服务器返回的第一个 IP 地址未绑定到任何网络接口卡 (NIC)，则上述遍历操作可能会用时较长。 连接到可用性组侦听器时，OLE DB 驱动程序的 SQL Server 将尝试并行建立与所有 IP 地址的连接，如果连接尝试成功，驱动程序将放弃所做的任何挂起的连接尝试。  
  
> [!NOTE]  
> 增大连接超时值和实现连接重试逻辑将增加应用程序连接到可用性组的概率。 此外，由于可用性组进行故障转移而可能使连接失败，您应实现连接重试逻辑，重试失败的连接，直至重新连接。  
  
## <a name="connecting-with-multisubnetfailover"></a>使用 MultiSubnetFailover 进行连接  
 始终指定**MultiSubnetFailover = Yes**当连接到 SQL Server Always On 可用性组侦听器或[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]故障转移群集实例。 **MultiSubnetFailover**为所有 Alwayson 可用性组和故障转移群集实例中启用更快的故障转移[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，并将显著减少单个和多子网 Alwayson 拓扑的故障转移时间。 在多子网故障转移过程中，客户端将尝试并行进行连接。 在子网故障转移时，OLE DB 驱动程序的 SQL Server 将重试 TCP 连接。  
  
 **MultiSubnetFailover**连接属性指示在可用性组或故障转移群集实例中部署应用程序和用于 SQL Server 的 OLE DB 驱动程序将尝试连接到数据库上主[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]实例尝试连接到所有 IP 地址。 为连接指定 **MultiSubnetFailover=Yes** 后，客户端将在比操作系统的默认 TCP 重传间隔更短的时间内重试 TCP 连接尝试。 这使的 Always On 可用性组或故障转移群集实例，更快地故障转移后的重新连接，适用于单-和多-subnet 可用性组和故障转移群集实例。  
  
 有关连接字符串关键字的详细信息，请参阅[OLE DB 驱动程序的 SQL Server 连接字符串关键字](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)。  
  
 如果在连接到非可用性组侦听程序或非故障转移群集实例时指定了 **MultiSubnetFailover=Yes**，可能会对性能造成负面影响，因此不支持这样做。  
  
 使用以下准则可以连接到可用性组或故障转移群集实例中的服务器：  
  
-   连接到单子网或多子网时使用 **MultiSubnetFailover** 连接属性，这二者的性能都会得到改进。  
  
-   若要连接到某一可用性组，请在您的连接字符串中将该可用性组的可用性组侦听器指定为服务器。  
  
-   连接到配置有超过 64 个 IP 地址的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例将导致连接失败。  
  
-   基于以下身份验证类型，使用 **MultiSubnetFailover** 连接属性的应用程序的行为不受影响：[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 身份验证、Kerberos 身份验证或 Windows 身份验证。  
  
-   你可以增加 **loginTimeout** 的值，以延长故障转移时间并减少应用程序连接重试次数。  
  
-   不支持分布式事务。  
  
如果只读路由不起作用，则连接到可用性组中的辅助副本位置在以下情况下将失败：  
  
1.  如果未将辅助副本位置配置为接受连接。  
  
2.  如果应用程序使用 **ApplicationIntent=ReadWrite**（在下文中介绍）且将次要副本位置配置为只读访问。  
  
如果将主副本配置为拒绝只读工作负荷且连接字符串包含 **ApplicationIntent=ReadOnly**，连接将失败。  
  
## <a name="upgrading-to-use-multi-subnet-clusters-from-database-mirroring"></a>升级以便使用来自数据库镜像的多子网群集  
如果连接字符串中已存在 **MultiSubnetFailover** 和 **Failover_Partner** 连接关键字，将出现连接错误。 如果使用 **MultiSubnetFailover** 且 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 返回一个故障转移伙伴响应指示它是数据库镜像对的一部分，也将出现错误。  
  
如果升级 SQL Server 应用程序用于 OLE DB 驱动程序当前使用数据库镜像到多子网方案，你应删除**Failover_Partner**连接属性并将其替换**MultiSubnetFailover**设置为**是**并将连接字符串中的服务器名称替换为可用性组侦听器。 如果连接字符串使用 **Failover_Partner** 和 **MultiSubnetFailover=Yes**，驱动程序将生成一个错误。 但是，如果连接字符串使用 **Failover_Partner** 和 **MultiSubnetFailover=No**（或 **ApplicationIntent=ReadWrite**），则该应用程序将使用数据库镜像。  
  
如果数据库镜像用于可用性组中的主数据库，并且 **MultiSubnetFailover=Yes** 用于连接到主数据库（而非连接到可用性组侦听程序）的连接字符串中，则驱动程序将返回错误。  


[!INCLUDE[specify-application-intent_read-only-routing](~/includes/paragraph-content/specify-application-intent-read-only-routing.md)]


## <a name="ole-db"></a>OLE DB  
SQL Server 的 OLE DB 驱动程序同时支持**ApplicationIntent**和**MultiSubnetFailover**关键字。   
  
添加了两个 OLE DB 连接字符串关键字，以支持[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]OLE DB 驱动程序中的 SQL Server:  
  
-   **ApplicationIntent** 
-   **MultiSubnetFailover**  
  
 SQL Server 的 OLE DB 驱动程序中的连接字符串关键字的详细信息，请参阅[OLE DB 驱动程序的 SQL Server 连接字符串关键字](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)。  

### <a name="application-intent"></a>应用程序意向 

等效的连接属性为：  
  
-   **SSPROP_INIT_APPLICATIONINTENT**  
  
-   **DBPROP_INIT_PROVIDERSTRING**  
  
SQL Server 应用程序用于 OLE DB 驱动程序可以使用一种方法来指定应用程序意向：  
  
 -   **Idbinitialize:: Initialize**  
 **IDBInitialize::Initialize** 使用以前配置的属性集来初始化数据源并创建数据源对象。 将应用程序意向指定为访问接口属性或作为扩展属性字符串的一部分。  
  
 -   **IDataInitialize::GetDataSource**  
 **IDataInitialize::GetDataSource** 使用可包含 **Application Intent** 关键字的输入连接字符串。  
  
 -   **IDBProperties::SetProperties**  
 若要设置 **ApplicationIntent** 属性值，请调用在带有“**ReadWrite**”或“**ReadOnly**”值的 **SSPROP_INIT_APPLICATIONINTENT** 属性或含有“**ApplicationIntent=ReadOnly**”或“**ApplicationIntent=ReadWrite**”值的 **DBPROP_INIT_PROVIDERSTRING** 属性中传递的 **IDBProperties::SetProperties**。  
  
可以在“数据链接属性”对话框的“全部”选项卡的“应用程序意向属性”字段中指定应用程序意向。  
  
建立隐式连接时，隐式连接将使用父连接的应用程序意向设置。 同样，从同一数据源创建的多个会话将继承数据源的应用程序意向设置。  
  
### <a name="multisubnetfailover"></a>MultiSubnetFailover

等效的连接属性为：  
  
-   **SSPROP_INIT_MULTISUBNETFAILOVER**  
  
-   **DBPROP_INIT_PROVIDERSTRING**  

SQL Server 应用程序用于 OLE DB 驱动程序可以使用以下方法之一设置 MultiSubnetFailover 选项：  

 -   **Idbinitialize:: Initialize**  
 **IDBInitialize::Initialize** 使用以前配置的属性集来初始化数据源并创建数据源对象。 将应用程序意向指定为访问接口属性或作为扩展属性字符串的一部分。  
  
 -   **IDataInitialize::GetDataSource**  
 **IDataInitialize::GetDataSource**采用输入的连接字符串可以包含**MultiSubnetFailover**关键字。  

-   **IDBProperties::SetProperties**  
若要设置**MultiSubnetFailover**属性值，请调用**IDBProperties::SetProperties**传入**SSPROP_INIT_MULTISUBNETFAILOVER**具有值属性**VARIANT_TRUE**或**VARIANT_FALSE**或**DBPROP_INIT_PROVIDERSTRING**属性值包含"**MultiSubnetFailover = Yes**"**MultiSubnetFailover = 否**"。

#### <a name="example"></a>示例

```
DBPROP rgPropMultisubnet;

rgPropMultisubnet.dwPropertyID = SSPROP_INIT_MULTISUBNETFAILOVER;
rgPropMultisubnet.dwOptions = DBPROPOPTIONS_REQUIRED;
rgPropMultisubnet.dwStatus = DBPROPSTATUS_OK;
rgPropMultisubnet.colid = DB_NULLID;
V_VT(&(rgPropMultisubnet.vValue)) = VT_BOOL;
V_BOOL(&(rgPropMultisubnet.vValue)) = VARIANT_TRUE;

DBPROPSET PropSet;

PropSet.rgProperties = &rgPropMultisubnet;
PropSet.cProperties = 1;
PropSet.guidPropertySet = DBPROPSET_SQLSERVERDBINIT;
IDBProperties* pIDBProperties = NULL;
hr = pIDBInitialize->QueryInterface(IID_IDBProperties, (void **)&pIDBProperties);
pIDBProperties->SetProperties(1, &PropSet);
```

## <a name="see-also"></a>请参阅  
 [用于 SQL Server 功能的 OLE DB 驱动程序](../../oledb/features/oledb-driver-for-sql-server-features.md)    
 [将连接字符串关键字与适用于 SQL Server 的 OLE DB 驱动程序结合使用](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)  
  
  
