---
title: 将连接字符串关键字与适用于 SQL Server 的 OLE DB 驱动程序结合使用 | Microsoft Docs
description: 将连接字符串关键字与适用于 SQL Server 的 OLE DB 驱动程序结合使用
ms.custom: ''
ms.date: 07/03/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
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
ms.author: pelopes
manager: craigg
ms.openlocfilehash: cbc464d86f77c609ecc53bc6ed02bb5fff60e3a8
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43026106"
---
# <a name="using-connection-string-keywords-with-ole-db-driver-for-sql-server"></a>将连接字符串关键字与适用于 SQL Server 的 OLE DB 驱动程序结合使用
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  SQL Server Api 的某些 OLE DB 驱动程序使用连接字符串来指定连接属性。 连接字符串是关键字和关联的值的列表；每个关键字标识特定的连接属性。  
  
> [!NOTE]
> 适用于 SQL Server 的 OLE DB 驱动程序允许连接字符串中存在多义性，以保持后向兼容性（例如，可以多次指定某些关键字，并且允许基于位置或优先级对发生冲突的关键字进行解析）。 OLE DB Driver for SQL Server 的未来版本可能不允许在连接字符串中的多义性。 在修改要使用适用于 SQL Server 的 OLE DB 驱动程序的应用程序时，最好消除连接字符串多义性上的任何依赖项。  
  
 以下部分介绍可用于 OLE DB 驱动程序与 SQL Server 和 ActiveX 数据对象 (ADO) 时为数据提供程序中使用 SQL Server 的 OLE DB 驱动程序的关键字。  

  
## <a name="ole-db-driver-connection-string-keywords"></a>OLE DB 驱动程序连接字符串关键字  
 OLE DB 应用程序可以用两种方式初始化数据源对象：  
  
-   **IDBInitialize::Initialize**  
  
-   **IDataInitialize::GetDataSource**  
  
 在第一种情况下，通过在 DBPROPSET_DBINIT 属性集中设置属性 DBPROP_INIT_PROVIDERSTRING，可以用访问接口字符串初始化连接属性。 在第二种情况下，可以将初始化字符串传递到 IDataInitialize::GetDataSource 方法以初始化连接属性。 两种方法都初始化相同的 OLE DB 连接属性，但使用不同的关键字集合。 IDataInitialize::GetDataSource 所使用的关键字集合至少是初始化属性组内的属性的说明。  
  
 将对应的 OLE DB 属性设置为某个默认值或显式设置为某个值的任何提供程序字符串设置，OLE DB 属性值将覆盖提供程序字符串中的设置。  
  
 通过 DBPROP_INIT_PROVIDERSTRING 值在访问接口字符串中所设置的布尔属性要使用值“yes”和“no”进行设置。 通过使用 IDataInitialize::GetDataSource 在初始化字符串中设置的布尔属性是使用值“true”和“false”进行设置的。  
  
 使用 IDataInitialize::GetDataSource 的应用程序也可以使用由 IDBInitialize::Initialize 使用的关键字，但仅用于没有默认值的属性。 如果应用程序在初始化字符串中同时使用 IDataInitialize::GetDataSource 关键字和 IDBInitialize::Initialize 关键字，则使用 IDataInitialize::GetDataSource 关键字设置。 强烈建议应用程序不要在 IDataInitialize:GetDataSource 连接字符串中使用 IDBInitialize::Initialize 关键字，因为在未来的版本中可能不保留该行为。  
  
> [!NOTE]  
>  通过 IDataInitialize::GetDataSource 传递的连接字符串将转换为属性并且通过 IDBProperties::SetProperties 应用。 如果组件服务在 IDBProperties::GetPropertyInfo 中找到了属性说明，则此属性将作为独立属性应用。 否则，它将通过 DBPROP_PROVIDERSTRING 属性应用。 例如，如果您指定连接字符串**数据源 = server1;Server = server2**，**数据源**将设置为一个属性，但**Server**将进入提供程序字符串。  
  
 如果指定访问接口特定的属性相同的多个实例，则使用第一个属性的第一个值。  
  
 将 IDBInitialize::Initialize 和 DBPROP_INIT_PROVIDERSTRING 配合使用的 OLE DB 应用程序所使用的连接字符串具有以下语法：  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=[{]attribute-value[}]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 属性值可以选择放在大括号中，并且最好这样做。 这样可以避免当属性值包含非字母数字字符时出现问题。 值中的第一个右大括号用于终止值，因此值不能包含右大括号。  
  
 连接字符串关键字的等号 (=) 之后的空白字符将被解释为文本，即使该值在引号内也是如此。  
  
 下表对可能与 DBPROP_INIT_PROVIDERSTRING 一起使用的关键字进行了说明。  
  
|关键字|初始化属性|描述|  
|-------------|-----------------------------|-----------------|  
|**Addr**|SSPROP_INIT_NETWORKADDRESS|“Address”的同义词。|  
|**Address**|SSPROP_INIT_NETWORKADDRESS|运行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的服务器的网络地址。 “Address”通常是服务器的网络名称，也可以是诸如管道、IP 地址或 TCP/IP 端口和套接字地址之类的其他名称。<br /><br /> 如果指定了 IP 地址，请确保在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 配置管理器中启用了 TCP/IP 或 named pipes 协议。<br /><br /> 值**地址**传递给的值的优先级高于**Server**在连接字符串时使用的 SQL Server OLE DB 驱动程序中。 另外请注意，`Address=;` 将连接到在 Server 关键字中指定的服务器，而 `Address= ;, Address=.;`、 `Address=localhost;` 和 `Address=(local);` 都会产生本地服务器的连接。<br /><br /> Address 关键字的完整语法如下所示：<br /><br /> [*协议 ***:**]* 地址 *[* *，* * * 端口&#124;\pipe\pipename*]<br /><br /> *protocol* 可以是 **tcp** (TCP/IP)、 **lpc** （共享内存）或 **np** （命名管道）。 有关协议的详细信息，请参阅[配置客户端协议](../../../database-engine/configure-windows/configure-client-protocols.md)。<br /><br /> 如果既没有*协议*也不**网络**指定关键字、 OLE DB 驱动程序适用于 SQL Server 将使用中指定的协议顺序[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]配置管理器。<br /><br /> “port”是指定服务器上所要连接到的端口。 默认情况下，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 使用端口 1433。|   
|**APP**|SSPROP_INIT_APPNAME|用于标识应用程序的字符串。|  
|**ApplicationIntent**|SSPROP_INIT_APPLICATIONINTENT|连接到服务器时声明应用程序工作负荷类型。 可能的值为 ReadOnly 和 ReadWrite。<br /><br /> 默认值是**ReadWrite**。 有关 OLE DB 驱动程序有关的 SQL Server 支持的详细信息[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]，请参阅[OLE DB 驱动程序对高可用性和灾难恢复的 SQL Server 支持](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)。|  
|**AttachDBFileName**|SSPROP_INIT_FILENAME|可附加数据库的主文件的名称（包括完整路径名）。 若要使用 AttachDBFileName，还必须使用访问接口字符串 Database 关键字来指定数据库名称。 如果该数据库以前已经附加，则 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不会重新附加它（而是使用已附加的数据库作为连接的默认数据库）。|  
|**自动翻译**|SSPROP_INIT_AUTOTRANSLATE|“AutoTranslate”的同义词。|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|配置 OEM/ANSI 字符转换。 可识别的值为“yes”和“no”。|  
|**“数据库”**|DBPROP_INIT_CATALOG|数据库名称。|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|指定要使用的数据类型的处理模式。 对于访问接口数据类型，可识别的值为“0”，对于 SQL Server 2000 数据类型则为“80”。|  
|**Encrypt**|SSPROP_INIT_ENCRYPT|指定在通过网络发送数据之前是否应当将其加密。 可能的值为“yes”和“no”。 默认值为“no”。|  
|**FailoverPartner**|SSPROP_INIT_FAILOVERPARTNER|用于数据库镜像的故障转移服务器的名称。|  
|**FailoverPartnerSPN**|SSPROP_INIT_FAILOVERPARTNERSPN|故障转移伙伴的 SPN。 默认值为空字符串。 空字符串导致 OLE DB 驱动程序的 SQL Server 以使用默认设置，提供程序生成的 SPN。|  
|**语言**|SSPROPT_INIT_CURRENTLANGUAGE|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 语言。|  
|**MarsConn**|SSPROP_INIT_MARSCONNECTION|如果服务器是 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 或更高版本，则启用或禁用连接上的多个活动结果集 (MARS)。 可能的值为“yes”和“no”。 默认值为“no”。|  
|**MultiSubnetFailover**|SSPROP_INIT_MULTISUBNETFAILOVER|在连接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可用性组或 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 故障转移群集实例的可用性组侦听程序时，应始终指定 MultiSubnetFailover=Yes。 MultiSubnetFailover=Yes 将配置适用于 SQL Server 的 OLE DB 驱动程序以便更快地检测和连接到（当前）活动服务器。 可能的值为“是”和“否”。 默认值为 No。 例如：<br /><br /> `MultiSubnetFailover=Yes`<br /><br /> 有关 OLE DB 驱动程序有关的 SQL Server 支持的详细信息[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]，请参阅[OLE DB 驱动程序对高可用性和灾难恢复的 SQL Server 支持](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)。|  
|**Net**|SSPROP_INIT_NETWORKLIBRARY|“Network”的同义词。|  
|**Network**|SSPROP_INIT_NETWORKLIBRARY|用于与组织中的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例建立连接的网络库。|  
|**Network Library**|SSPROP_INIT_NETWORKLIBRARY|“Network”的同义词。|  
|**PacketSize**|SSPROP_INIT_PACKETSIZE|网络数据包大小。 默认值为 4096。|  
|**PersistSensitive**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|接受字符串“yes”和“no”作为值。 如果是“no”，则不允许数据源对象保留敏感的身份验证信息。|  
|**PWD**|DBPROP_AUTH_PASSWORD|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登录密码。|  
|**Server**|DBPROP_INIT_DATASOURCE|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的名称。 该值必须是服务器的网络名称、IP 地址或者 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 配置管理器别名。<br /><br /> 如果不指定，则与本地计算机上的默认实例建立连接。<br /><br /> **地址**关键字将覆盖**Server**关键字。<br /><br /> 通过指定以下条件之一，可连接到本地服务器的默认实例：<br /><br /> **Server =;**<br /><br /> **Server =。;**<br /><br /> **与;**<br /><br /> **与;**<br /><br /> **Server=(localhost);**<br /><br /> **Server=(localdb)\\**  *instancename* **;**<br /><br /> 有关 LocalDB 的支持的详细信息，请参阅[OLE DB 驱动程序对 LocalDB 的 SQL Server 支持](../../oledb/features/oledb-driver-for-sql-server-support-for-localdb.md)。<br /><br /> 若要指定的命名的实例[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，将追加 **\\ ***InstanceName *。<br /><br />时未指定服务器，则连接到本地计算机上的默认实例。<br /> <br />如果你指定的 IP 地址，请确保在启用了 TCP/IP 或 named 的 pipes 协议[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Configuration Manager。<br /><br />的完整语法**服务器**关键字是按如下所示：<br /> <br /> **Server =**[* 协议***:**]*服务器*[**，* * * 端口*]<br /><br /> *protocol* 可以是 **tcp** (TCP/IP)、 **lpc** （共享内存）或 **np** （命名管道）。<br /><br /> 以下示例将指定一个命名管道：<br /><br /> `np:\\.\pipe\MSSQL$MYINST01\sql\query`<br /><br /> 此行指定 named pipes 协议、本地计算机上的一个命名管道 (`\\.\pipe`)、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的名称 (`MSSQL$MYINST01`)，以及命名管道的默认名称 (`sql/query`)。<br /><br /> 如果既没有*协议*也不**网络**指定关键字、 OLE DB 驱动程序适用于 SQL Server 将使用中指定的协议顺序[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]配置管理器。<br /><br /> “port”是指定服务器上所要连接到的端口。 默认情况下，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 使用端口 1433。<br /><br /> 将忽略传递给的值开头的空格**Server**在连接字符串时使用的 SQL Server OLE DB 驱动程序中。|   
|**ServerSPN**|SSPROP_INIT_SERVERSPN|服务器的 SPN。 默认值为空字符串。 空字符串导致 OLE DB 驱动程序的 SQL Server 以使用默认设置，提供程序生成的 SPN。|  
|**超时**|DBPROP_INIT_TIMEOUT|等待数据源初始化完成的时间（秒）。|  
|**Trusted_Connection**|DBPROP_AUTH_INTEGRATED|何时"yes"，指示 SQL Server 的 OLE DB 驱动程序使用 Windows 身份验证模式进行登录验证。 否则指示适用于 SQL Server 的 OLE DB 驱动程序使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 用户名和密码进行登录验证，并且必须指定 UID 和 PWD 关键字。|  
|**TrustServerCertificate**|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|接受字符串“yes”和“no”作为值。 默认值为“no”，它意味着将验证服务器证书。|  
|**UID**|DBPROP_AUTH_USERID|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登录名。|  
|**UseFMTONLY**|SSPROP_INIT_USEFMTONLY|控制元数据的检索方式连接到时[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]和更高版本。 可能的值为“yes”和“no”。 默认值为“no”。<br /><br />默认情况下，使用 SQL Server 的 OLE DB 驱动程序[sp_describe_first_result_set](../../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md)并[sp_describe_undeclared_parameters](../../../relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql.md)存储过程来检索元数据。 这些存储的过程有一些限制 （例如它们将失败时在临时表上）。 设置**UseFMTONLY**为"yes"指示驱动程序以使用[SET FMTONLY](../../../t-sql/statements/set-fmtonly-transact-sql.md)进行元数据检索相反。|  
|**UseProcForPrepare**|SSPROP_INIT_USEPROCFORPREP|此关键字已弃用，并且 SQL Server 的 OLE DB 驱动程序将忽略其设置。|  
|**WSID**|SSPROP_INIT_WSID|工作站标识符。|  
  
 使用 IDataInitialize::GetDataSource 的 OLE DB 应用程序所使用的连接字符串有以下语法：  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=[quote]attribute-value[quote]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 `quote ::= " | '`  
  
 属性使用必须符合其作用域中允许的语法。  例如， **WSID**使用大括号 (**{}**) 引号字符并**应用程序名称**使用单引号 () 或双精度 (**"**) 引号字符。 只有字符串属性可以加引号。 尝试将整数或枚举属性用引号引起来将导致“连接字符串不符合 OLE DB 规范”错误。  
  
 属性值可以选择放在单引号或双引号内，并且最好这样做。 这样可以避免当值包含非字母数字字符时出现问题。 也可以在值内使用引号字符，只要使用的是双引号。  
  
 连接字符串关键字的等号 (=) 之后的空白字符将被解释为文本，即使该值在引号内也是如此。  
  
 如果某一连接字符串具有下表所列的多个属性，将使用最后一个属性的值。  
  
 下表对可能与 IDataInitialize::GetDataSource 配合使用的关键字进行了说明：  
  
|关键字|初始化属性|描述|  
|-------------|-----------------------------|-----------------|  
|**应用程序名称**|SSPROP_INIT_APPNAME|用于标识应用程序的字符串。|  
|**Application Intent**|SSPROP_INIT_APPLICATIONINTENT|连接到服务器时声明应用程序工作负荷类型。 可能的值为 ReadOnly 和 ReadWrite。<br /><br /> 默认值是**ReadWrite**。 有关 OLE DB 驱动程序有关的 SQL Server 支持的详细信息[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]，请参阅[OLE DB 驱动程序对高可用性和灾难恢复的 SQL Server 支持](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)。|  
|**自动翻译**|SSPROP_INIT_AUTOTRANSLATE|“AutoTranslate”的同义词。|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|配置 OEM/ANSI 字符转换。 可识别的值为“true”和“false”。|  
|**Connect Timeout**|DBPROP_INIT_TIMEOUT|等待数据源初始化完成的时间（秒）。|  
|**Current Language**|SSPROPT_INIT_CURRENTLANGUAGE|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 语言名称。|  
|**数据源**|DBPROP_INIT_DATASOURCE|组织中的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的名称。<br /><br /> 如果不指定，则与本地计算机上的默认实例建立连接。<br /><br /> 若要详细了解有效的地址语法，请参阅本主题中的 Server 关键字说明。|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|指定要使用的数据类型的处理模式。 可识别的值对访问接口数据类型为“0”，对 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 数据类型为“80”。|  
|**Failover Partner**|SSPROP_INIT_FAILOVERPARTNER|用于数据库镜像的故障转移服务器的名称。|  
|**Failover Partner SPN**|SSPROP_INIT_FAILOVERPARTNERSPN|故障转移伙伴的 SPN。 默认值为空字符串。 空字符串导致 OLE DB 驱动程序的 SQL Server 以使用默认设置，提供程序生成的 SPN。|  
|**初始目录**|DBPROP_INIT_CATALOG|数据库名称。|  
|**初始文件名**|SSPROP_INIT_FILENAME|可附加数据库的主文件的名称（包括完整路径名）。 若要使用 AttachDBFileName，还必须使用访问接口字符串 DATABASE 关键字来指定数据库名称。 如果该数据库以前已经附加，则 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不会重新附加它（而是使用已附加的数据库作为连接的默认数据库）。|  
|**Integrated Security**|DBPROP_AUTH_INTEGRATED|接受 Windows 身份验证的值“SSPI”。|  
|**MARS Connection**|SSPROP_INIT_MARSCONNECTION|启用或禁用连接上的多个活动结果集 (MARS)。 可识别的值为“true”和“false”。 默认值为“false”。|  
|**MultiSubnetFailover**|SSPROP_INIT_MULTISUBNETFAILOVER|在连接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可用性组或 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 故障转移群集实例的可用性组侦听程序时，应始终指定 MultiSubnetFailover=True。 MultiSubnetFailover=True 将配置适用于 SQL Server 的 OLE DB 驱动程序，以便更快地检测和连接到（当前）活动服务器。 可能的值包括 **True** 和 **False**。 默认值为 **False**。 例如：<br /><br /> `MultiSubnetFailover=True`<br /><br /> 有关 OLE DB 驱动程序有关的 SQL Server 支持的详细信息[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]，请参阅[OLE DB 驱动程序对高可用性和灾难恢复的 SQL Server 支持](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)。|  
|**Network Address**|SSPROP_INIT_NETWORKADDRESS|组织中的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的网络地址。<br /><br /> 若要详细了解有效的地址语法，请参阅本主题中的 Address 关键字说明。|  
|**Network Library**|SSPROP_INIT_NETWORKLIBRARY|用于与组织中的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例建立连接的网络库。|  
|**Packet Size**|SSPROP_INIT_PACKETSIZE|网络数据包大小。 默认值为 4096。|  
|**密码**|DBPROP_AUTH_PASSWORD|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登录密码。|  
|**Persist Security Info**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|接受字符串“true”和“false”作为值。 如果是“false”，则不允许数据源对象保留敏感的身份验证信息|  
|**提供程序**||对于 OLE DB 驱动程序适用于 SQL Server，这应该是"MSOLEDBSQL"。|  
|**Server SPN**|SSPROP_INIT_SERVERSPN|服务器的 SPN。 默认值为空字符串。 空字符串导致 OLE DB 驱动程序的 SQL Server 以使用默认设置，提供程序生成的 SPN。|  
|**信任服务器证书**|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|接受字符串“true”和“false”作为值。 默认值为“false”，它意味着将验证服务器证书。|  
|**Use Encryption for Data**|SSPROP_INIT_ENCRYPT|指定在通过网络发送数据之前是否应当将其加密。 可能的值为“true”和“false”。 默认值为“false”。|  
|**Use FMTONLY**|SSPROP_INIT_USEFMTONLY|控制元数据的检索方式连接到时[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]和更高版本。 可能的值为“true”和“false”。 默认值为“false”。<br /><br />默认情况下，使用 SQL Server 的 OLE DB 驱动程序[sp_describe_first_result_set](../../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md)并[sp_describe_undeclared_parameters](../../../relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql.md)存储过程来检索元数据。 这些存储的过程有一些限制 （例如它们将失败时在临时表上）。 设置**使用 FMTONLY**来"true"指示驱动程序以使用[SET FMTONLY](../../../t-sql/statements/set-fmtonly-transact-sql.md)进行元数据检索相反。|  
|**用户 ID**|DBPROP_AUTH_USERID|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登录名。|  
|**Workstation ID**|SSPROP_INIT_WSID|工作站标识符。|  
  
 **注意**：在连接字符串中，“旧密码”属性会设置 SSPROP_AUTH_OLD_PASSWORD，它是当前密码（可能已过期），通过访问接口字符串属性无法获取该密码。  
  
## <a name="activex-data-objects-ado-connection-string-keywords"></a>ActiveX 数据对象 (ADO) 连接字符串关键字  
 ADO 应用程序设置 ADODBConnection 对象的 ConnectionString 属性，或提供连接字符串作为 ADODBConnection 对象的 Open 方法的参数。  
  
 ADO 应用程序还可以使用由 OLE DB IDBInitialize::Initialize 方法使用的关键字，但仅针对没有默认值的属性。 如果应用程序在初始化字符串中同时使用这些 ADO 关键字和 IDBInitialize::Initialize 关键字，则使用 ADO 关键字设置。 强烈建议应用程序仅使用 ADO 连接字符串关键字。  
  
 ADO 使用的连接字符串有以下语法：  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=["]attribute-value["]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 属性值可以选择放在双引号中，并且最好这样做。 这样可以避免当值包含非字母数字字符时出现问题。 属性值不能包含双引号。  
  
 下表对可能与 ADO 连接字符串一起使用的关键字进行了说明：  
  
|关键字|初始化属性|描述|  
|-------------|-----------------------------|-----------------|  
|**Application Intent**|SSPROP_INIT_APPLICATIONINTENT|连接到服务器时声明应用程序工作负荷类型。 可能的值为 ReadOnly 和 ReadWrite。<br /><br /> 默认值是**ReadWrite**。 有关 OLE DB 驱动程序有关的 SQL Server 支持的详细信息[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]，请参阅[OLE DB 驱动程序对高可用性和灾难恢复的 SQL Server 支持](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)。|  
|**应用程序名称**|SSPROP_INIT_APPNAME|用于标识应用程序的字符串。|  
|**自动翻译**|SSPROP_INIT_AUTOTRANSLATE|“AutoTranslate”的同义词。|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|配置 OEM/ANSI 字符转换。 可识别的值为“true”和“false”。|  
|**Connect Timeout**|DBPROP_INIT_TIMEOUT|等待数据源初始化完成的时间（秒）。|  
|**Current Language**|SSPROPT_INIT_CURRENTLANGUAGE|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 语言名称。|  
|**数据源**|DBPROP_INIT_DATASOURCE|组织中的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的名称。<br /><br /> 如果不指定，则与本地计算机上的默认实例建立连接。<br /><br /> 若要详细了解有效的地址语法，请参阅本主题中的 Server 关键字说明。|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|指定将使用的数据类型的处理模式。 对于访问接口数据类型，可识别的值为“0”，对于 SQL Server 2000 数据类型则为“80”。|  
|**Failover Partner**|SSPROP_INIT_FAILOVERPARTNER|用于数据库镜像的故障转移服务器的名称。|  
|**Failover Partner SPN**|SSPROP_INIT_FAILOVERPARTNERSPN|故障转移伙伴的 SPN。 默认值为空字符串。 空字符串导致 OLE DB 驱动程序的 SQL Server 以使用默认设置，提供程序生成的 SPN。|  
|**初始目录**|DBPROP_INIT_CATALOG|数据库名称。|  
|**初始文件名**|SSPROP_INIT_FILENAME|可附加数据库的主文件的名称（包括完整路径名）。 若要使用 AttachDBFileName，还必须使用访问接口字符串 DATABASE 关键字来指定数据库名称。 如果该数据库以前已经附加，则 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不会重新附加它（而是使用已附加的数据库作为连接的默认数据库）。|  
|**Integrated Security**|DBPROP_AUTH_INTEGRATED|接受 Windows 身份验证的值“SSPI”。|  
|**MARS Connection**|SSPROP_INIT_MARSCONNECTION|如果服务器是 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 或更高版本，则启用或禁用连接上的多个活动结果集 (MARS)。 可识别的值为“true”和“false”。默认值为“false”。|  
|**MultiSubnetFailover**|SSPROP_INIT_MULTISUBNETFAILOVER|在连接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 可用性组或 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 故障转移群集实例的可用性组侦听程序时，应始终指定 MultiSubnetFailover=True。 MultiSubnetFailover=True 将配置适用于 SQL Server 的 OLE DB 驱动程序，以便更快地检测和连接到（当前）活动服务器。 可能的值包括 **True** 和 **False**。 默认值为 **False**。 例如：<br /><br /> `MultiSubnetFailover=True`<br /><br /> 有关 OLE DB 驱动程序有关的 SQL Server 支持的详细信息[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]，请参阅[OLE DB 驱动程序对高可用性和灾难恢复的 SQL Server 支持](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)。|  
|**Network Address**|SSPROP_INIT_NETWORKADDRESS|组织中的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的网络地址。<br /><br /> 若要详细了解有效的地址语法，请参阅本主题中的 Address 关键字说明。|  
|**Network Library**|SSPROP_INIT_NETWORKLIBRARY|用于与组织中的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例建立连接的网络库。|  
|**Packet Size**|SSPROP_INIT_PACKETSIZE|网络数据包大小。 默认值为 4096。|  
|**密码**|DBPROP_AUTH_PASSWORD|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登录密码。|  
|**Persist Security Info**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|接受字符串“true”和“false”作为值。 如果是“false”，则不允许数据源对象保留敏感的身份验证信息。|  
|**提供程序**||对于 OLE DB 驱动程序适用于 SQL Server，这应该是"MSOLEDBSQL"。|  
|**Server SPN**|SSPROP_INIT_SERVERSPN|服务器的 SPN。 默认值为空字符串。 空字符串导致 OLE DB 驱动程序的 SQL Server 以使用默认设置，提供程序生成的 SPN。|  
|**信任服务器证书**|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|接受字符串“true”和“false”作为值。 默认值为“false”，它意味着将验证服务器证书。|  
|**Use Encryption for Data**|SSPROP_INIT_ENCRYPT|指定在通过网络发送数据之前是否应当将其加密。 可能的值为“true”和“false”。 默认值为“false”。|  
|**Use FMTONLY**|SSPROP_INIT_USEFMTONLY|控制元数据的检索方式连接到时[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]和更高版本。 可能的值为“true”和“false”。 默认值为“false”。<br /><br />默认情况下，使用 SQL Server 的 OLE DB 驱动程序[sp_describe_first_result_set](../../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md)并[sp_describe_undeclared_parameters](../../../relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql.md)存储过程来检索元数据。 这些存储的过程有一些限制 （例如它们将失败时在临时表上）。 设置**使用 FMTONLY**来"true"指示驱动程序以使用[SET FMTONLY](../../../t-sql/statements/set-fmtonly-transact-sql.md)进行元数据检索相反。|  
|**用户 ID**|DBPROP_AUTH_USERID|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登录名。|  
|**Workstation ID**|SSPROP_INIT_WSID|工作站标识符。|  
  
 **注意**：在连接字符串中，“旧密码”属性会设置 SSPROP_AUTH_OLD_PASSWORD，它是当前密码（可能已过期），通过访问接口字符串属性无法获取该密码。  
  
## <a name="see-also"></a>另请参阅  
 [使用适用于 SQL Server 的 OLE DB 驱动程序生成应用程序](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
  
  
