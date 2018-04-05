---
title: 将连接字符串关键字用于 OLE DB 驱动程序适用于 SQL Server |Microsoft 文档
description: 将连接字符串关键字用于 OLE DB 驱动程序适用于 SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- sql13.swb.connecttoserver.options.registeredservers.f1
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], connection string keywords
- MSOLEDBSQL, connection string keywords
- connection strings [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, connection string keywords
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 7917f0c1344ff8e79250791d1b262cece9ca3c4c
ms.sourcegitcommit: 8b332c12850c283ae413e0b04b2b290ac2edb672
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/05/2018
---
# <a name="using-connection-string-keywords-with-ole-db-driver-for-sql-server"></a>将连接字符串关键字用于 OLE DB 驱动程序适用于 SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  用于 SQL Server Api 某些 OLE DB 驱动程序使用连接字符串指定连接属性。 连接字符串是关键字和关联的值的列表；每个关键字标识特定的连接属性。  
  
> **注意：** OLE DB 驱动程序的 SQL Server 允许在连接字符串以保持向后兼容的多义性 (例如，可能会超过一次，指定某些关键字和冲突关键字可能允许基于位置的解析或优先级）。 OLE DB 驱动程序的 SQL Server 的未来版本可能不允许在连接字符串中的多义性。 修改应用程序以使用 OLE DB 驱动程序的 SQL Server 以消除任何依赖于连接字符串多义性时，它是很好的做法。  
  
 以下各节描述了可与 OLE DB 驱动程序的 SQL Server 和 ActiveX 数据对象 (ADO) 时使用的数据提供程序作为 OLE DB 驱动程序的 SQL Server 的关键字。  

  
## <a name="ole-db-driver-connection-string-keywords"></a>OLE DB 驱动程序连接字符串关键字  
 OLE DB 应用程序可以用两种方式初始化数据源对象：  
  
-   **Idbinitialize:: Initialize**  
  
-   **IDataInitialize::GetDataSource**  
  
 在第一种情况下，通过在 DBPROPSET_DBINIT 属性集中设置属性 DBPROP_INIT_PROVIDERSTRING，可以用访问接口字符串初始化连接属性。 在第二个情况下，可以将初始化字符串传递给**IDataInitialize::GetDataSource**方法以初始化连接属性。 两种方法都初始化相同的 OLE DB 连接属性，但使用不同的关键字集合。 使用关键字的一套**IDataInitialize::GetDataSource**至少是初始化属性组中的属性的说明。  
  
 将对应的 OLE DB 属性设置为某个默认值或显式设置为某个值的任何提供程序字符串设置，OLE DB 属性值将覆盖提供程序字符串中的设置。  
  
 通过 DBPROP_INIT_PROVIDERSTRING 值在访问接口字符串中所设置的布尔属性要使用值“yes”和“no”进行设置。 在使用的初始化字符串中设置的布尔属性**IDataInitialize::GetDataSource**使用的值"true"和"false"设置。  
  
 使用应用程序**IDataInitialize::GetDataSource**还可以使用使用的关键字**idbinitialize:: Initialize**但仅针对不具有默认值的属性。 如果应用程序使用这两个**IDataInitialize::GetDataSource**关键字和**idbinitialize:: Initialize**初始化字符串中的关键字**IDataInitialize::GetDataSource**使用关键字设置。 强烈建议应用程序，不使用**idbinitialize:: Initialize**中的关键字**IDataInitialize:GetDataSource**连接字符串，此行为可能未维护在将来版本。  
  
> [!NOTE]  
>  连接字符串传递**IDataInitialize::GetDataSource**会转换为属性和应用通过**IDBProperties::SetProperties**。 如果找到组件服务中的属性说明**IDBProperties::GetPropertyInfo**，此属性将应用作为独立属性。 否则，它将通过 DBPROP_PROVIDERSTRING 属性应用。 例如，如果您指定连接字符串**数据源 = server1;服务器 = server2**，**数据源**将设置为一个属性，但**服务器**将传递给提供程序字符串。  
  
 如果指定多个实例相同的提供程序特定属性，将使用第一个属性的第一个值。  
  
 使用的 OLE DB 应用程序使用 DBPROP_INIT_PROVIDERSTRING 与连接字符串**idbinitialize:: Initialize**具有以下语法：  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=[{]attribute-value[}]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 属性值可以选择放在大括号中，并且最好这样做。 这样可以避免当属性值包含非字母数字字符时出现问题。 值中的第一个右大括号用于终止值，因此值不能包含右大括号。  
  
 空格字符后将被解释为文本，连接字符串关键字的 = 符号，即使值用引号引起来。  
  
 下表对可能与 DBPROP_INIT_PROVIDERSTRING 一起使用的关键字进行了说明。  
  
|关键字|初始化属性|Description|  
|-------------|-----------------------------|-----------------|  
|**Addr**|SSPROP_INIT_NETWORKADDRESS|“Address”的同义词。|  
|**Address**|SSPROP_INIT_NETWORKADDRESS|运行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的服务器的网络地址。 **地址**通常是网络服务器的名称，但可以是管道、 IP 地址或 TCP/IP 端口和套接字地址等其他名称。<br /><br /> 如果指定了 IP 地址，请确保在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 配置管理器中启用了 TCP/IP 或 named pipes 协议。<br /><br /> 值**地址**优先于传递给值**服务器**在连接字符串时使用的 SQL Server OLE DB 驱动程序。 另请注意，`Address=;`将连接到中指定的服务器**服务器**关键字，而`Address= ;, Address=.;`， `Address=localhost;`，和`Address=(local);`所有会导致与本地服务器的连接。<br /><br /> 完整语法**地址**关键字是，如下所示：<br /><br /> [*协议 ***:**]*地址*[* *，* * * 端口&#124;\pipe\pipename*]<br /><br /> *protocol* 可以是 **tcp** (TCP/IP)、 **lpc** （共享内存）或 **np** （命名管道）。 有关协议的详细信息，请参阅[Configure Client Protocols](../../../database-engine/configure-windows/configure-client-protocols.md)。<br /><br /> 如果既没有*协议*也不**网络**指定关键字，OLE DB 驱动程序的 SQL Server 将使用中指定的协议顺序[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Configuration Manager。<br /><br /> *端口*是要连接到指定的服务器上的端口。 默认情况下，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 使用端口 1433。|   
|**APP**|SSPROP_INIT_APPNAME|用于标识应用程序的字符串。|  
|**ApplicationIntent**|SSPROP_INIT_APPLICATIONINTENT|连接到服务器时声明应用程序工作负荷类型。 可能的值为**ReadOnly**和**ReadWrite**。<br /><br /> 默认值是**ReadWrite**。 有关 OLE DB 驱动程序有关的 SQL Server 支持的详细信息[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]，请参阅[OLE DB 驱动程序的 SQL 服务器支持对高可用性、 灾难恢复](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)。|  
|**AttachDBFileName**|SSPROP_INIT_FILENAME|可附加数据库的主文件的名称（包括完整路径名）。 若要使用**AttachDBFileName**，还必须使用提供程序字符串数据库关键字指定数据库名称。 如果该数据库以前已经附加，则 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不会重新附加它（而是使用已附加的数据库作为连接的默认数据库）。|  
|**自动翻译**|SSPROP_INIT_AUTOTRANSLATE|“AutoTranslate”的同义词。|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|配置 OEM/ANSI 字符转换。 可识别的值为“yes”和“no”。|  
|**数据库**|DBPROP_INIT_CATALOG|数据库名称。|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|指定要使用的数据类型的处理模式。 对于访问接口数据类型，可识别的值为“0”，对于 SQL Server 2000 数据类型则为“80”。|  
|**Encrypt**|SSPROP_INIT_ENCRYPT|指定在通过网络发送数据之前是否应当将其加密。 可能的值为“yes”和“no”。 默认值为“no”。|  
|**FailoverPartner**|SSPROP_INIT_FAILOVERPARTNER|用于数据库镜像的故障转移服务器的名称。|  
|**FailoverPartnerSPN**|SSPROP_INIT_FAILOVERPARTNERSPN|故障转移伙伴的 SPN。 默认值为空字符串。 空字符串会导致 OLE DB 驱动程序的 SQL Server 以使用默认情况下，提供程序生成的 SPN。|  
|**语言**|SSPROPT_INIT_CURRENTLANGUAGE|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 语言。|  
|**MarsConn**|SSPROP_INIT_MARSCONNECTION|如果服务器是 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 或更高版本，则启用或禁用连接上的多个活动结果集 (MARS)。 可能的值为“yes”和“no”。 默认值为“no”。|  
|**MultiSubnetFailover**|SSPROP_INIT_MULTISUBNETFAILOVER|始终指定**MultiSubnetFailover = Yes**连接到的可用性组侦听器时[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]可用性组或[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]故障转移群集实例。 **MultiSubnetFailover = Yes**配置 OLE DB 驱动程序的 SQL Server 以更快地检测和连接到 （当前） 活动服务器。 可能的值为“是”和“否”。 默认值是**否**。 例如：<br /><br /> `MultiSubnetFailover=Yes`<br /><br /> 有关 OLE DB 驱动程序有关的 SQL Server 支持的详细信息[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]，请参阅[OLE DB 驱动程序的 SQL 服务器支持对高可用性、 灾难恢复](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)。|  
|**Net**|SSPROP_INIT_NETWORKLIBRARY|“Network”的同义词。|  
|**网络**|SSPROP_INIT_NETWORKLIBRARY|用于与组织中的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例建立连接的网络库。|  
|**网络库**|SSPROP_INIT_NETWORKLIBRARY|“Network”的同义词。|  
|**PacketSize**|SSPROP_INIT_PACKETSIZE|网络数据包大小。 默认值为 4096。|  
|**PersistSensitive**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|接受字符串“yes”和“no”作为值。 如果是“no”，则不允许数据源对象保留敏感的身份验证信息。|  
|**PWD**|DBPROP_AUTH_PASSWORD|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登录密码。|  
|**Server**|DBPROP_INIT_DATASOURCE|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的名称。 该值必须是服务器的网络名称、IP 地址或者 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 配置管理器别名。<br /><br /> 如果不指定，则与本地计算机上的默认实例建立连接。<br /><br /> **地址**关键字覆盖**服务器**关键字。<br /><br /> 通过指定以下项之一，你可以连接到本地服务器上的默认实例：<br /><br /> **Server=;**<br /><br /> **Server=.;**<br /><br /> **Server=(local);**<br /><br /> **Server=(local);**<br /><br /> **Server=(localhost);**<br /><br /> **Server=(localdb)\\** *instancename* **;**<br /><br /> 有关 LocalDB 的支持的详细信息，请参阅[OLE DB 驱动程序为对 LocalDB 的 SQL Server 支持](../../oledb/features/oledb-driver-for-sql-server-support-for-localdb.md)。<br /><br /> 若要指定的命名的实例[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，追加 **\\ ***InstanceName*。<br /><br />指定没有服务器时，将本地计算机上的默认实例建立连接。<br /><br />如果指定的 IP 地址，请确保在中启用了 TCP/IP 或命名的管道协议[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Configuration Manager。<br /><br />完整语法**服务器**关键字，如下所示是：<br /> <br /> **Server =**[*协议***:**]*服务器*[**，* * * 端口*]<br /><br /> *protocol* 可以是 **tcp** (TCP/IP)、 **lpc** （共享内存）或 **np** （命名管道）。<br /><br /> 以下示例将指定一个命名管道：<br /><br /> `np:\\.\pipe\MSSQL$MYINST01\sql\query`<br /><br /> 此行指定 named pipes 协议、本地计算机上的一个命名管道 (`\\.\pipe`)、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的名称 (`MSSQL$MYINST01`)，以及命名管道的默认名称 (`sql/query`)。<br /><br /> 如果既没有*协议*也不**网络**指定关键字，OLE DB 驱动程序的 SQL Server 将使用中指定的协议顺序[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Configuration Manager。<br /><br /> *端口*是要连接到指定的服务器上的端口。 默认情况下，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 使用端口 1433。<br /><br /> 传递给的值的开头将忽略空格**服务器**在连接字符串时使用的 SQL Server OLE DB 驱动程序。|   
|**ServerSPN**|SSPROP_INIT_SERVERSPN|服务器的 SPN。 默认值为空字符串。 空字符串会导致 OLE DB 驱动程序的 SQL Server 以使用默认情况下，提供程序生成的 SPN。|  
|**超时**|DBPROP_INIT_TIMEOUT|等待数据源初始化完成的时间（秒）。|  
|**Trusted_Connection**|DBPROP_AUTH_INTEGRATED|何时"是"，指示 SQL Server 的 OLE DB 驱动程序用于 Windows 身份验证模式进行登录验证。 否则指示用于 SQL Server 以使用 OLE DB 驱动程序[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]必须指定用户名和密码登录验证和 UID 和 PWD 关键字。|  
|**TrustServerCertificate**|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|接受字符串“yes”和“no”作为值。 默认值为“no”，它意味着将验证服务器证书。|  
|**UID**|DBPROP_AUTH_USERID|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]登录名。|  
|**UseProcForPrepare**|SSPROP_INIT_USEPROCFORPREP|此关键字被弃用，并且其设置适用于 SQL Server 将忽略 OLE DB 驱动程序。|  
|**WSID**|SSPROP_INIT_WSID|工作站标识符。|  
  
 使用 OLE DB 应用程序使用的连接字符串**IDataInitialize::GetDataSource**具有以下语法：  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=[quote]attribute-value[quote]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 `quote ::= " | '`  
  
 属性使用必须符合其作用域中允许的语法。  例如， **WSID**使用大括号 (**{}**) 引号字符和**应用程序名称**使用单 () 或双引号 (**"**) 引号字符。 只有字符串属性可以加引号。 尝试将整数或枚举属性用引号引起来将导致“连接字符串不符合 OLE DB 规范”错误。  
  
 属性值可以选择放在单引号或双引号内，并且最好这样做。 这样可以避免当值包含非字母数字字符时出现问题。 也可以在值内使用引号字符，只要使用的是双引号。  
  
 空格字符后将被解释为文本，连接字符串关键字的 = 符号，即使值用引号引起来。  
  
 如果某一连接字符串具有下表所列的多个属性，将使用最后一个属性的值。  
  
 下表介绍可用于的关键字**IDataInitialize::GetDataSource**:  
  
|关键字|初始化属性|Description|  
|-------------|-----------------------------|-----------------|  
|**应用程序名称**|SSPROP_INIT_APPNAME|用于标识应用程序的字符串。|  
|**应用程序意向**|SSPROP_INIT_APPLICATIONINTENT|连接到服务器时声明应用程序工作负荷类型。 可能的值为**ReadOnly**和**ReadWrite**。<br /><br /> 默认值是**ReadWrite**。 有关 OLE DB 驱动程序有关的 SQL Server 支持的详细信息[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]，请参阅[OLE DB 驱动程序的 SQL 服务器支持对高可用性、 灾难恢复](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)。|  
|**自动翻译**|SSPROP_INIT_AUTOTRANSLATE|“AutoTranslate”的同义词。|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|配置 OEM/ANSI 字符转换。 可识别的值为“true”和“false”。|  
|**Connect Timeout**|DBPROP_INIT_TIMEOUT|等待数据源初始化完成的时间（秒）。|  
|**当前语言**|SSPROPT_INIT_CURRENTLANGUAGE|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 语言名称。|  
|**数据源**|DBPROP_INIT_DATASOURCE|组织中的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的名称。<br /><br /> 如果不指定，则与本地计算机上的默认实例建立连接。<br /><br /> 有关有效的地址语法的详细信息，请参阅的说明**服务器**关键字，本主题中的。|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|指定要使用的数据类型的处理模式。 可识别的值对访问接口数据类型为“0”，对 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 数据类型为“80”。|  
|**Failover Partner**|SSPROP_INIT_FAILOVERPARTNER|用于数据库镜像的故障转移服务器的名称。|  
|**故障转移伙伴 SPN**|SSPROP_INIT_FAILOVERPARTNERSPN|故障转移伙伴的 SPN。 默认值为空字符串。 空字符串会导致 OLE DB 驱动程序的 SQL Server 以使用默认情况下，提供程序生成的 SPN。|  
|**初始目录**|DBPROP_INIT_CATALOG|数据库名称。|  
|**初始文件名**|SSPROP_INIT_FILENAME|可附加数据库的主文件的名称（包括完整路径名）。 若要使用**AttachDBFileName**，还必须使用提供程序字符串数据库关键字指定数据库名称。 如果该数据库以前已经附加，则 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不会重新附加它（而是使用已附加的数据库作为连接的默认数据库）。|  
|**Integrated Security**|DBPROP_AUTH_INTEGRATED|接受 Windows 身份验证的值“SSPI”。|  
|**MARS 连接**|SSPROP_INIT_MARSCONNECTION|启用或禁用连接上的多个活动结果集 (MARS)。 可识别的值为“true”和“false”。 默认值为“false”。|  
|**MultiSubnetFailover**|SSPROP_INIT_MULTISUBNETFAILOVER|始终指定**MultiSubnetFailover = True**连接到的可用性组侦听器时[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]可用性组或[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]故障转移群集实例。 **MultiSubnetFailover = True**配置 OLE DB 驱动程序的 SQL Server 以更快地检测和连接到 （当前） 活动服务器。 可能的值包括 **True** 和 **False**。 默认值为 **False**。 例如：<br /><br /> `MultiSubnetFailover=True`<br /><br /> 有关 OLE DB 驱动程序有关的 SQL Server 支持的详细信息[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]，请参阅[OLE DB 驱动程序的 SQL 服务器支持对高可用性、 灾难恢复](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)。|  
|**网络地址**|SSPROP_INIT_NETWORKADDRESS|组织中的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的网络地址。<br /><br /> 有关有效的地址语法的详细信息，请参阅的说明**地址**关键字，本主题中的。|  
|**网络库**|SSPROP_INIT_NETWORKLIBRARY|用于与组织中的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例建立连接的网络库。|  
|**Packet Size**|SSPROP_INIT_PACKETSIZE|网络数据包大小。 默认值为 4096。|  
|**密码**|DBPROP_AUTH_PASSWORD|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登录密码。|  
|**持久性安全信息**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|接受字符串“true”和“false”作为值。 当"false"时，不允许数据源对象来保持敏感的身份验证信息|  
|**提供程序**||对于 OLE DB 驱动程序的 SQL Server，这应该是"MSOLEDBSQL"。|  
|**服务器 SPN**|SSPROP_INIT_SERVERSPN|服务器的 SPN。 默认值为空字符串。 空字符串会导致 OLE DB 驱动程序的 SQL Server 以使用默认情况下，提供程序生成的 SPN。|  
|**信任服务器证书**|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|接受字符串“true”和“false”作为值。 默认值为“false”，它意味着将验证服务器证书。|  
|**Use Encryption for Data**|SSPROP_INIT_ENCRYPT|指定在通过网络发送数据之前是否应当将其加密。 可能的值为“true”和“false”。 默认值为"false"。|  
|**用户 ID**|DBPROP_AUTH_USERID|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]登录名。|  
|**工作站 ID**|SSPROP_INIT_WSID|工作站标识符。|  
  
 **请注意**连接字符串中的"旧密码"属性设置 SSPROP_AUTH_OLD_PASSWORD，这是不是可通过提供程序字符串属性的当前 （可能已过期） 密码。  
  
## <a name="activex-data-objects-ado-connection-string-keywords"></a>ActiveX 数据对象 (ADO) 连接字符串关键字  
 ADO 应用程序集**ConnectionString**属性**ADODBConnection**对象，或在提供一个连接字符串作为参数传递给**打开**方法**ADODBConnection**对象。  
  
 ADO 应用程序还可以使用 OLE DB 所使用的关键字**idbinitialize:: Initialize**方法，但只针对不具有默认值的属性。 如果应用程序使用 ADO 关键字和**idbinitialize:: Initialize**将使用在初始化字符串中，设置 ADO 关键字的关键字。 强烈建议应用程序仅使用 ADO 连接字符串关键字。  
  
 ADO 使用的连接字符串有以下语法：  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=["]attribute-value["]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 属性值可以选择放在双引号中，并且最好这样做。 这样可以避免当值包含非字母数字字符时出现问题。 属性值不能包含双引号。  
  
 下表对可能与 ADO 连接字符串一起使用的关键字进行了说明：  
  
|关键字|初始化属性|Description|  
|-------------|-----------------------------|-----------------|  
|**应用程序意向**|SSPROP_INIT_APPLICATIONINTENT|连接到服务器时声明应用程序工作负荷类型。 可能的值为**ReadOnly**和**ReadWrite**。<br /><br /> 默认值是**ReadWrite**。 有关 OLE DB 驱动程序有关的 SQL Server 支持的详细信息[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]，请参阅[OLE DB 驱动程序的 SQL 服务器支持对高可用性、 灾难恢复](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)。|  
|**应用程序名称**|SSPROP_INIT_APPNAME|用于标识应用程序的字符串。|  
|**自动翻译**|SSPROP_INIT_AUTOTRANSLATE|“AutoTranslate”的同义词。|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|配置 OEM/ANSI 字符转换。 可识别的值为“true”和“false”。|  
|**Connect Timeout**|DBPROP_INIT_TIMEOUT|等待数据源初始化完成的时间（秒）。|  
|**当前语言**|SSPROPT_INIT_CURRENTLANGUAGE|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 语言名称。|  
|**数据源**|DBPROP_INIT_DATASOURCE|组织中的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的名称。<br /><br /> 如果不指定，则与本地计算机上的默认实例建立连接。<br /><br /> 有关有效的地址语法的详细信息，请参阅的说明**服务器**关键字，本主题中的。|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|指定将使用的数据类型的处理模式。 对于访问接口数据类型，可识别的值为“0”，对于 SQL Server 2000 数据类型则为“80”。|  
|**Failover Partner**|SSPROP_INIT_FAILOVERPARTNER|用于数据库镜像的故障转移服务器的名称。|  
|**故障转移伙伴 SPN**|SSPROP_INIT_FAILOVERPARTNERSPN|故障转移伙伴的 SPN。 默认值为空字符串。 空字符串会导致 OLE DB 驱动程序的 SQL Server 以使用默认情况下，提供程序生成的 SPN。|  
|**初始目录**|DBPROP_INIT_CATALOG|数据库名称。|  
|**初始文件名**|SSPROP_INIT_FILENAME|可附加数据库的主文件的名称（包括完整路径名）。 若要使用**AttachDBFileName**，还必须使用提供程序字符串数据库关键字指定数据库名称。 如果该数据库以前已经附加，则 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不会重新附加它（而是使用已附加的数据库作为连接的默认数据库）。|  
|**Integrated Security**|DBPROP_AUTH_INTEGRATED|接受 Windows 身份验证的值“SSPI”。|  
|**MARS 连接**|SSPROP_INIT_MARSCONNECTION|如果服务器是 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 或更高版本，则启用或禁用连接上的多个活动结果集 (MARS)。 可识别的值为“true”和“false”。默认值为“false”。|  
|**MultiSubnetFailover**|SSPROP_INIT_MULTISUBNETFAILOVER|始终指定**MultiSubnetFailover = True**连接到的可用性组侦听器时[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]可用性组或[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]故障转移群集实例。 **MultiSubnetFailover = True**配置 OLE DB 驱动程序的 SQL Server 以更快地检测和连接到 （当前） 活动服务器。 可能的值包括 **True** 和 **False**。 默认值为 **False**。 例如：<br /><br /> `MultiSubnetFailover=True`<br /><br /> 有关 OLE DB 驱动程序有关的 SQL Server 支持的详细信息[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]，请参阅[OLE DB 驱动程序的 SQL 服务器支持对高可用性、 灾难恢复](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)。|  
|**网络地址**|SSPROP_INIT_NETWORKADDRESS|组织中的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的网络地址。<br /><br /> 有关有效的地址语法的详细信息，请参阅的说明**地址**关键字，本主题中的。|  
|**网络库**|SSPROP_INIT_NETWORKLIBRARY|用于与组织中的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例建立连接的网络库。|  
|**Packet Size**|SSPROP_INIT_PACKETSIZE|网络数据包大小。 默认值为 4096。|  
|**密码**|DBPROP_AUTH_PASSWORD|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登录密码。|  
|**持久性安全信息**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|接受字符串“true”和“false”作为值。 如果是“false”，则不允许数据源对象保留敏感的身份验证信息。|  
|**提供程序**||对于 OLE DB 驱动程序的 SQL Server，这应该是"MSOLEDBSQL"。|  
|**服务器 SPN**|SSPROP_INIT_SERVERSPN|服务器的 SPN。 默认值为空字符串。 空字符串会导致 OLE DB 驱动程序的 SQL Server 以使用默认情况下，提供程序生成的 SPN。|  
|**信任服务器证书**|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|接受字符串“true”和“false”作为值。 默认值为“false”，它意味着将验证服务器证书。|  
|**Use Encryption for Data**|SSPROP_INIT_ENCRYPT|指定在通过网络发送数据之前是否应当将其加密。 可能的值为“true”和“false”。 默认值为"false"。|  
|**用户 ID**|DBPROP_AUTH_USERID|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]登录名。|  
|**工作站 ID**|SSPROP_INIT_WSID|工作站标识符。|  
  
 **请注意**连接字符串中的"旧密码"属性设置 SSPROP_AUTH_OLD_PASSWORD，这是不是可通过提供程序字符串属性的当前 （可能已过期） 密码。  
  
## <a name="see-also"></a>另请参阅  
 [使用适用于 SQL Server 的 OLE DB 驱动程序生成应用程序](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
  
  
