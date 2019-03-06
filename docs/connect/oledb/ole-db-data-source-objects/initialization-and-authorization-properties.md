---
title: 初始化和授权属性 |Microsoft Docs
description: 初始化和授权属性
ms.custom: ''
ms.date: 02/06/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- authorization [OLE DB]
- properties [OLE DB]
- OLE DB Driver for SQL Server, initialization properties
- OLE DB Driver for SQL Server, authorization properties
- initialization properties [OLE DB]
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: a2477e18f1ae9aa78d195a45f28494b4b909934d
ms.sourcegitcommit: 958cffe9288cfe281280544b763c542ca4025684
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 02/23/2019
ms.locfileid: "56744517"
---
# <a name="initialization-and-authorization-properties"></a>初始化和授权属性
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  SQL Server 的 OLE DB 驱动程序，如下所示解释 OLE DB 初始化和授权属性：  
  
|属性 ID|描述|  
|-----------------|-----------------|  
|DBPROP_AUTH_CACHE_AUTHINFO|SQL Server 的 OLE DB 驱动程序不会缓存身份验证信息。<br /><br /> SQL Server 的 OLE DB 驱动程序在尝试设置属性值将返回 DB_S_ERRORSOCCURRED。 DBPROP 结构的 dwStatus 成员指示 DBPROPSTATUS_NOTSUPPORTED。|  
|DBPROP_AUTH_ENCRYPT_PASSWORD|SQL Server 的 OLE DB 驱动程序使用标准[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]安全机制来隐藏密码。<br /><br /> SQL Server 的 OLE DB 驱动程序在尝试设置属性值将返回 DB_S_ERRORSOCCURRED。 DBPROP 结构的 dwStatus 成员指示 DBPROPSTATUS_NOTSUPPORTED。|  
|DBPROP_AUTH_INTEGRATED|如果 DBPROP_AUTH_INTEGRATED 设置为空指针、Null 字符串或“SSPI”VT_BSTR 值，则适用于 SQL Server 的 OLE DB 驱动程序使用 Windows 身份验证模式来授权用户访问由 DBPROP_INIT_DATASOURCE 和 DBPROP_INIT_CATALOG 属性指定的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库。<br /><br /> 如果它设置为 VT_EMPTY（默认值），则使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安全机制。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登录和密码是在 DBPROP_AUTH_USERID 和 DBPROP_AUTH_PASSWORD 属性中指定的。|  
|DBPROP_AUTH_MASK_PASSWORD|SQL Server 的 OLE DB 驱动程序使用标准[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]安全机制来隐藏密码。<br /><br /> SQL Server 的 OLE DB 驱动程序在尝试设置属性值将返回 DB_S_ERRORSOCCURRED。 DBPROP 结构的 dwStatus 成员指示 DBPROPSTATUS_NOTSUPPORTED。|  
|DBPROP_AUTH_PASSWORD|分配给 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登录名的密码。 选用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 身份验证来授权访问 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库时，将使用该属性。|  
|DBPROP_AUTH_PERSIST_ENCRYPTED|SQL Server 的 OLE DB 驱动程序不会加密身份验证信息，如果保持不变。<br /><br /> SQL Server 的 OLE DB 驱动程序在尝试设置属性值将返回 DB_S_ERRORSOCCURRED。 DBPROP 结构的 dwStatus 成员指示 DBPROPSTATUS_NOTSUPPORTED。|  
|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|必要时，适用于 SQL Server 的 OLE DB 驱动程序将永久保存身份验证值，例如密码的图像。 不提供加密。|  
|DBPROP_AUTH_USERID|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登录名。 选用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 身份验证来授权访问 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库时，将使用该属性。|  
|DBPROP_INIT_ASYNCH|SQL Server 的 OLE DB 驱动程序支持异步启动。<br /><br /> 如果设置 DBPROP_INIT_ASYNCH 属性中的 DBPROPVAL_ASYNCH_INITIALIZE 位，将导致 IDBInitialize::Initialize 成为非阻止调用。 有关详细信息，请参阅[正在执行异步操作](../../oledb/features/performing-asynchronous-operations.md)。|  
|DBPROP_INIT_CATALOG|要连接的现有 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库的名称。|  
|DBPROP_INIT_DATASOURCE|运行 [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的服务器的网络名称。 如果计算机上运行了 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的多个实例，则需要按 \\\ServerName\InstanceName 的形式指定 DBPROP_INIT_DATASOURCE 值，以连接到特定的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例。 转义序列 \\\ 表示反斜杠自身。|  
|DBPROP_INIT_GENERALTIMEOUT|指示请求（数据源初始化和命令执行除外）超时前等待的时间（秒）。如果值为 0，则表示无限期超时。通过网络连接工作或者在分布式或事务处理情况下工作的访问接口可以支持该属性，以便在遇到长时间运行的请求时建议登记的组件触发超时。 数据源初始化和命令执行的超时仍分别由 DBPROP_INIT_TIMEOUT 和 DBPROP_COMMANDTIMEOUT 控制。<br /><br /> DBPROP_INIT_GENERALTIMEOUT 是只读的；如果尝试设置它，将返回 dwstatus 错误 DBPROPSTATUS_NOTSETTABLE。|  
|DBPROP_INIT_HWND|来自调用应用程序的 Windows 句柄。 如果允许提示用户输入初始化属性，则必须有有效的窗口句柄，才能显示初始化对话框。|  
|DBPROP_INIT_IMPERSONATION_LEVEL|SQL Server 的 OLE DB 驱动程序不支持模拟级别调整。<br /><br /> SQL Server 的 OLE DB 驱动程序在尝试设置属性值将返回 DB_S_ERRORSOCCURRED。 DBPROP 结构的 dwStatus 成员指示 DBPROPSTATUS_NOTSUPPORTED。|  
|DBPROP_INIT_LCID|适用于 SQL Server 的 OLE DB 驱动程序验证区域设置 ID；如果区域设置 ID 不受支持或未在客户端上安装，则返回错误。|  
|DBPROP_INIT_LOCATION|SQL Server 的 OLE DB 驱动程序在尝试设置属性值将返回 DB_S_ERRORSOCCURRED。 DBPROP 结构的 dwStatus 成员指示 DBPROPSTATUS_NOTSUPPORTED。|  
|DBPROP_INIT_MODE|SQL Server 的 OLE DB 驱动程序在尝试设置属性值将返回 DB_S_ERRORSOCCURRED。 DBPROP 结构的 dwStatus 成员指示 DBPROPSTATUS_NOTSUPPORTED。|  
|DBPROP_INIT_PROMPT|SQL Server 的 OLE DB 驱动程序支持数据源初始化的所有提示模式。 SQL Server 的 OLE DB 驱动程序使用 DBPROMPT_NOPROMPT 作为其默认设置的属性。|  
|DBPROP_INIT_PROTECTION_LEVEL|SQL Server 的 OLE DB 驱动程序不支持连接到的实例上的保护级别[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。<br /><br /> SQL Server 的 OLE DB 驱动程序在尝试设置属性值将返回 DB_S_ERRORSOCCURRED。 DBPROP 结构的 dwStatus 成员指示 DBPROPSTATUS_NOTSUPPORTED。|  
|DBPROP_INIT_PROVIDERSTRING|请参阅本主题后面的 SQL Server 字符串，OLE DB 驱动程序。|  
|DBPROP_INIT_TIMEOUT|如果无法在指定的秒数内建立与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的连接，则适用于 SQL Server 的 OLE DB 驱动程序在初始化时返回错误。|  
  
 在提供程序特定的属性集 DBPROPSET_SQLSERVERDBINIT 中，适用于 SQL Server 的 OLE DB 驱动程序定义这些额外的初始化属性。  
  
|属性 ID|描述|  
|-----------------|-----------------|  
|SSPROP_AUTH_ACCESS_TOKEN<a href="#table1_1"><sup>**1**</sup></a>|类型：VT_BSTR<br /><br /> R/W：读/写<br /><br /> 默认值：VT_EMPTY<br /><br /> 说明： 使用向 Azure Active Directory 进行身份验证的访问令牌。 <br/><br/>**注意：** 是错误来指定此属性，也`UID`， `PWD`， `Trusted_Connection`，或`Authentication`连接字符串关键字或其相应的属性/关键字。|
|SSPROP_AUTH_MODE<a href="#table1_1"><sup>**1**</sup></a>|类型：VT_BSTR<br /><br /> R/W：读/写<br /><br /> 默认值：VT_EMPTY<br /><br /> 说明： 指定使用的 SQL 或 Active Directory 身份验证。 有效值为<br/><ul><li>`(not set)`： 由其他关键字身份验证模式。</li><li>`(empty string)`： 取消设置以前设置身份验证模式。</li><li>`ActiveDirectoryPassword:` Active Directory 身份验证使用登录 ID 和密码。</li><li>`ActiveDirectoryIntegrated:` 对使用当前登录的用户的 Windows 帐户凭据的 Active Directory 集成身份验证。</li><br/>**注意：** 它具有**建议**使用该应用程序`Integrated Security`(或`Trusted_Connection`) 身份验证关键字或其对应的属性的值设置`Authentication`关键字 （或其相应的属性） 到`ActiveDirectoryIntegrated`若要启用新的加密和证书验证行为。<br/><br/><li>`SqlPassword:` 使用登录 ID 和密码进行身份验证。</li><br/>**注意：** 它具有**建议**使用该应用程序`SQL Server`身份验证设置的值`Authentication`关键字 （或其相应的属性） 到`SqlPassword`若要启用新的加密和证书验证行为。</ul>|
|SSPROP_AUTH_OLD_PASSWORD|类型：VT_BSTR<br /><br /> R/W：写<br /><br /> 默认值：VT_EMPTY<br /><br /> 说明：当前或过期的密码。 有关详细信息，请参阅[更改密码以编程方式](../../oledb/features/changing-passwords-programmatically.md)。|  
|SSPROP_INIT_APPNAME|类型：VT_BSTR<br /><br /> R/W：读/写<br /><br /> 说明：客户端应用程序名称。|  
|SSPROP_INIT_AUTOTRANSLATE|类型：VT_BOOL<br /><br /> R/W：读/写<br /><br /> 默认值：VARIANT_TRUE<br /><br /> 说明：OEM/ANSI 字符转换。<br /><br /> VARIANT_TRUE：适用于 SQL Server 的 OLE DB 驱动程序通过 Unicode 转换来转换在客户端和服务器之间发送的 ANSI 字符串，从而将客户端和服务器的代码页之间匹配的扩展字符中的问题降低最少：<br /><br /> 对于发送到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]char、varchar 或 text 变量、参数或列实例的客户端 DBTYPE_STR 数据，它们先使用客户端 ANSI 代码页 (ACP) 从字符转换到 Unicode，再使用服务器的 ACP 从 Unicode 转换到字符。<br /><br /> 对于发送到客户端 DBTYPE_STR 变量的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] char、varchar 或 text 数据，它们使用服务器 ACP 从字符转换到 Unicode，再使用客户端 ACP 从 Unicode 转换到字符。<br /><br /> 这些转换适用于 SQL Server 执行客户端上通过 OLE DB 驱动程序。 这要求客户端上有在服务器上使用的同一 ACP。<br /><br /> 这些设置对于为下面这些传输而发生的转换无效：<br /><br /> 发送到服务器上的 char、varchar 或 text 的 Unicode DBTYPE_WSTR 客户端数据。<br /><br /> 发送到客户端上的 Unicode DBTYPE_WSTR 变量的 char、varchar 或 text 服务器数据。<br /><br /> 发送到服务器上的 Unicode nchar、nvarchar 或 ntext 的 ANSI DBTYPE_STR 客户端数据。<br /><br /> 发送到客户端上的 ANSI DBTYPE_STR 变量的 Unicode char、varchar 或 text 服务器数据。<br /><br /> VARIANT_FALSE: SQL Server 的 OLE DB 驱动程序不执行字符转换。<br /><br /> 对于发送到服务器上的 char、varchar 或 text 变量、参数或列的客户端 ANSI 字符 DBTYPE_STR 数据，适用于 SQL Server 的 OLE DB 驱动程序不进行转换。 对于从服务器发送到客户端上的 DBTYPE_STR 变量的 char、varchar 或 text 数据，不执行转换。<br /><br /> 如果客户端和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例正在使用不同的 ACP，可能会错误地解释扩展字符。|  
|SSPROP_INIT_CURRENTLANGUAGE|类型：VT_BSTR<br /><br /> R/W：读/写<br /><br /> 说明：[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 语言名称。 标识用于系统消息选择和格式化的语言。 必须在运行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的计算机上安装该语言，否则数据源初始化将失败。|  
|SSPROP_INIT_DATATYPECOMPATIBILITY|类型：VT_UI2<br /><br /> R/W：读/写<br /><br /> 默认值：0<br /><br /> 说明：在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 和 ActiveX 数据对象 (ADO) 应用程序之间实现数据类型兼容。 如果使用默认值 0，则数据类型处理将默认采用由访问接口使用的方案。 如果使用值 80，则数据类型处理仅使用 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 数据类型。 有关详细信息，请参阅[使用 ADO 与 OLE DB 驱动程序适用于 SQL Server](../../oledb/applications/using-ado-with-oledb-driver-for-sql-server.md)。|  
|SSPROP_INIT_ENCRYPT<a href="#table1_1"><sup>**1**</sup></a>|类型：VT_BOOL<br /><br /> R/W：读/写<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明：若要加密通过网络传输的数据，应将 SSPROP_INIT_ENCRYPT 属性设置为 VARIANT_TRUE。<br /><br /> 如果启用了“强制协议加密”，则不论 SSPROP_INIT_ENCRYPT 如何设置，始终都会进行加密。 如果将它关闭，并将 SSPROP_INIT_ENCRYPT 设置为 VARIANT_TRUE，那么将进行加密。<br /><br /> 如果关闭了“强制协议加密”，并将 SSPROP_INIT_ENCRYPT 设置为 VARIANT_FALSE，那么不进行加密。|  
|SSPROP_INIT_FAILOVERPARTNER|类型：VT_BSTR<br /><br /> R/W：读/写<br /><br /> 说明：指定用于数据库镜像的故障转移伙伴的名称。 它是初始化属性，并且只能在初始化之前设置。 在初始化之后，它将返回由主服务器返回的故障转移伙伴（如果有）。<br /><br /> 这允许智能应用程序缓存最新确定的备份服务器，但这样的应用程序应当知道，仅当初次建立（对于池连接则是重置）连接时该信息才会更新，因而在经过长时间的连接后可能会过时。<br /><br /> 建立连接之后，应用程序可以查询该属性，以确定故障转移伙伴的标识。 如果主服务器没有故障转移伙伴，则此属性将返回空字符串。 有关详细信息，请参阅[使用数据库镜像](../../oledb/features/using-database-mirroring.md)。|  
|SSPROP_INIT_FILENAME|类型：VT_BSTR<br /><br /> R/W：读/写<br /><br /> 说明：指定可附加数据库的主文件名。 附加此数据库并使其成为连接的默认数据库。 若要使用 SSPROP_INIT_FILENAME，必须指定该数据库的名称作为初始化属性 DBPROP_INIT_CATALOG 的值。 如果该数据库名称不存在，它将查找在 SSPROP_INIT_FILENAME 中指定的主文件名，并使用在 DBPROP_INIT_CATALOG 中指定的名称来附加该数据库。 如果数据库是以前附加的，则 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不重新附加它。|  
|SSPROP_INIT_MARSCONNECTION|类型：VT_BOOL<br /><br /> R/W：读/写<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明：指定是否对连接启用多个活动结果集 (MARS)。 必须在与数据库建立连接之前将该选项设置为 true。 有关详细信息，请参阅[使用多个活动的结果集 (MARS)](../../oledb/features/using-multiple-active-result-sets-mars.md)。|  
|SSPROP_INIT_NETWORKADDRESS|类型：VT_BSTR<br /><br /> R/W：读/写<br /><br /> 说明：运行由 DBPROP_INIT_DATASOURCE 属性指定的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的服务器的网络地址。|  
|SSPROP_INIT_NETWORKLIBRARY|类型：VT_BSTR<br /><br /> R/W：读/写<br /><br /> 说明：用于与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例通信的网络库 (DLL) 的名称。 该名称不应当包含路径或 .dll 文件扩展名。<br /><br /> 可以使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 客户端配置实用工具来自定义其默认值。<br /><br /> 注意：该属性仅支持 TCP 和 Named Pipes。 如果该属性在使用时带有前缀，最后将得到导致错误的双前缀，因为该属性用于在内部生成前缀。|  
|SSPROP_INIT_PACKETSIZE|类型：VT_I4<br /><br /> R/W：读/写<br /><br /> 说明：以字节为单位表示的网络数据包大小。 数据包大小属性值必须介于 512 和 32,767 之间。 默认 OLE DB 驱动程序的 SQL Server 网络数据包大小为 4,096。|  
|SSPROP_INIT_TAGCOLUMNCOLLATION|类型：BOOL<br /><br /> R/W：写<br /><br /> 默认值：FALSE<br /><br /> 说明：使用服务器端游标时，在数据库更新期间使用。 该属性用从服务器而不是客户端上的代码页获得的排序规则信息来标记数据。 当前，该属性仅供分布式查询进程使用，因为它知道目标数据的排序规则，并能正确转换它。|  
|SSPROP_INIT_TRUST_SERVER_CERTIFICATE<a href="#table1_1"><sup>**1**</sup></a>|类型：VT_BOOL<br /><br /> R/W：读/写<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明：用于启用或禁用服务器证书验证。 该属性是读/写属性，但在已建立连接之后尝试设置它将导致错误。<br /><br /> 如果客户端配置为要求进行证书验证，则忽略该属性。 但是，应用程序可以将它与 SSPROP_INIT_ENCRYPT 一起使用，以保证即使将客户端配置为不要求加密，并且客户端上不提供证书，仍然会对应用程序与服务器之间的连接进行加密。<br /><br /> 客户端应用程序可以在打开连接后查询此属性，以确定使用的实际加密和验证设置。<br /><br /> 注意：如果加密但不验证证书，则可针对数据包探查提供部分防护，但不防护中间人攻击。 它只是允许对发送到服务器的登录名和数据进行加密，而无需验证服务器证书。<br /><br /> 有关详细信息，请参阅[使用加密但不验证](../../oledb/features/using-encryption-without-validation.md)。|  
|SSPROP_INIT_USEPROCFORPREP|类型：VT_I4<br /><br /> R/W：读/写<br /><br /> 默认值：SSPROPVAL_USEPROCFORPREP_ON<br /><br /> 说明：[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 存储过程的使用情况。 定义 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 临时存储过程的使用，以支持 ICommandPrepare 接口。 仅当连接到 SQL Server 6.5 时，该属性才有意义。 对于更高版本，将忽略该属性。<br /><br /> SSPROPVAL_USEPROCFORPREP_OFF：准备命令时，不创建临时存储过程。<br /><br /> SSPROPVAL_USEPROCFORPREP_ON：准备命令时，创建临时存储过程。 释放会话时，删除临时存储过程。<br /><br /> SSPROPVAL_USEPROCFORPREP_ON_DROP：准备命令时，创建临时存储过程。 使用 ICommandPrepare::Unprepare 撤销命令时，使用 ICommandText::SetCommandText 为命令对象指定新命令时，或释放对命令的所有应用程序引用时，删除该过程。|  
|SSPROP_INIT_WSID|类型：VT_BSTR<br /><br /> R/W：读/写<br /><br /> 说明：用于标识工作站的字符串。|  
  

<b id="table1_1">[1]:</b>为了提高安全性，加密和证书验证行为修改时使用的身份验证/访问令牌初始化属性或其相应的连接字符串关键字。 有关详细信息，请参阅[加密和证书验证](../features/using-azure-active-directory.md#encryption-and-certificate-validation)。

 在提供程序特定的属性集 DBPROPSET_SQLSERVERDATASOURCEINFO 中，SQL Server 的 OLE DB 驱动程序定义的其他属性;请参阅[数据源信息属性](../../oledb/ole-db-data-source-objects/data-source-information-properties.md)有关详细信息。  
  
## <a name="the-ole-db-driver-for-sql-server-string"></a>适用于 SQL Server 的 OLE DB 驱动程序字符串  
 SQL Server 的 OLE DB 驱动程序可以识别在提供程序字符串属性值中类似 ODBC 的语法。 在建立与 OLE DB 数据源的连接时，访问接口字符串属性将作为 OLE DB 初始化属性 DBPROP_INIT_PROVIDERSTRING 的值提供。 该属性指定在实现与 OLE DB 数据源的连接时所需的特定于 OLE DB 访问接口的连接数据。 在字符串中，各元素是使用分号分隔的。 字符串中的最后一个元素必须以分号结束。 每个元素均由一个关键字、一个等号字符和在初始化时传递的值组成。 例如：  
  
```  
Server=MyServer;UID=MyUserName;  
```  
  
 使用 OLE DB 驱动程序适用于 SQL Server，使用者永远不需要使用访问接口字符串属性。 通过使用 OLE DB 或适用于 SQL Server 的 OLE DB 驱动程序特定的初始化属性，使用者可设置在提供程序字符串中反映的所有初始化属性。  
  
 SQL Server 的 OLE DB 驱动程序中可用关键字的列表，请参阅[OLE DB 驱动程序适用于 SQL Server 连接字符串关键字](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)。  
  
## <a name="see-also"></a>另请参阅  
 [数据源对象&#40;OLE DB&#41;](../../oledb/ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
