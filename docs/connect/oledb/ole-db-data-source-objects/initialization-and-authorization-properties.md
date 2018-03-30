---
title: 初始化和授权属性 |Microsoft 文档
description: 初始化和授权属性
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-data-source-objects
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- authorization [OLE DB]
- properties [OLE DB]
- OLE DB Driver for SQL Server, initialization properties
- OLE DB Driver for SQL Server, authorization properties
- initialization properties [OLE DB]
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6be9ab05f9f7a5c669e62f92c238be3d06dbf44d
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2018
---
# <a name="initialization-and-authorization-properties"></a>初始化和授权属性
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  SQL Server 的 OLE DB 驱动程序将 OLE DB 初始化和授权属性的解释，如下所示：  
  
|属性 ID|Description|  
|-----------------|-----------------|  
|DBPROP_AUTH_CACHE_AUTHINFO|SQL Server 的 OLE DB 驱动程序不会缓存身份验证信息。<br /><br /> SQL Server 的 OLE DB 驱动程序返回 DB_S_ERRORSOCCURRED 尝试设置属性值。 *DwStatus*需要的 DBPROP 结构中的成员指示 DBPROPSTATUS_NOTSUPPORTED。|  
|DBPROP_AUTH_ENCRYPT_PASSWORD|SQL Server 的 OLE DB 驱动程序使用标准[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]掩盖密码的安全机制。<br /><br /> SQL Server 的 OLE DB 驱动程序返回 DB_S_ERRORSOCCURRED 尝试设置属性值。 *DwStatus*需要的 DBPROP 结构中的成员指示 DBPROPSTATUS_NOTSUPPORTED。|  
|DBPROP_AUTH_INTEGRATED|如果 DBPROP_AUTH_INTEGRATED 设置为指针为 NULL、 空字符串或 SSPI VT_BSTR 值，用于 SQL Server 的 OLE DB 驱动程序将使用 Windows 身份验证模式来授予用户访问权限[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]由 DBPROP_INIT_DATASOURCE 和需要的 DBPROP 指定的数据库_INIT_CATALOG 属性。<br /><br /> 如果它设置为 VT_EMPTY（默认值），则使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 安全机制。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登录和密码是在 DBPROP_AUTH_USERID 和 DBPROP_AUTH_PASSWORD 属性中指定的。|  
|DBPROP_AUTH_MASK_PASSWORD|SQL Server 的 OLE DB 驱动程序使用标准[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]掩盖密码的安全机制。<br /><br /> SQL Server 的 OLE DB 驱动程序返回 DB_S_ERRORSOCCURRED 尝试设置属性值。 *DwStatus*需要的 DBPROP 结构中的成员指示 DBPROPSTATUS_NOTSUPPORTED。|  
|DBPROP_AUTH_PASSWORD|分配给 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登录名的密码。 选用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 身份验证来授权访问 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库时，将使用该属性。|  
|DBPROP_AUTH_PERSIST_ENCRYPTED|SQL Server 的 OLE DB 驱动程序不加密身份验证信息如果保持不变。<br /><br /> SQL Server 的 OLE DB 驱动程序返回 DB_S_ERRORSOCCURRED 尝试设置属性值。 *DwStatus*需要的 DBPROP 结构中的成员指示 DBPROPSTATUS_NOTSUPPORTED。|  
|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|SQL Server 的 OLE DB 驱动程序仍然存在身份验证值，如果请求为此，包括密码的映像。 不提供加密。|  
|DBPROP_AUTH_USERID|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登录名。 选用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 身份验证来授权访问 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库时，将使用该属性。|  
|DBPROP_INIT_ASYNCH|SQL Server 的 OLE DB 驱动程序支持异步启动。<br /><br /> 设置位 DBPROP_INIT_ASYNCH 属性会导致在 DBPROPVAL_ASYNCH_INITIALIZE **idbinitialize:: Initialize**成为非阻止调用。 有关详细信息，请参阅[执行异步操作](../../oledb/features/performing-asynchronous-operations.md)。|  
|DBPROP_INIT_CATALOG|要连接的现有 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据库的名称。|  
|DBPROP_INIT_DATASOURCE|运行的实例的服务器的网络名称[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 如果有多个实例的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]运行的计算机上，以便在连接到的特定实例[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]DBPROP_INIT_DATASOURCE 指定为值 *\\\ServerName\InstanceName*。 转义序列\\\ 用于反斜杠本身。|  
|DBPROP_INIT_GENERALTIMEOUT|指示请求（数据源初始化和命令执行除外）超时前等待的时间（秒）。如果值为 0，则表示无限期超时。通过网络连接工作或者在分布式或事务处理情况下工作的访问接口可以支持该属性，以便在遇到长时间运行的请求时建议登记的组件触发超时。 数据源初始化和命令执行的超时仍分别由 DBPROP_INIT_TIMEOUT 和 DBPROP_COMMANDTIMEOUT 控制。<br /><br /> DBPROP_INIT_GENERALTIMEOUT 是只读的并且如果有人尝试将其设置*dwstatus*返回的 DBPROPSTATUS_NOTSETTABLE 错误。|  
|DBPROP_INIT_HWND|来自调用应用程序的 Windows 句柄。 如果允许提示用户输入初始化属性，则必须有有效的窗口句柄，才能显示初始化对话框。|  
|DBPROP_INIT_IMPERSONATION_LEVEL|SQL Server 的 OLE DB 驱动程序不支持模拟级别调整。<br /><br /> SQL Server 的 OLE DB 驱动程序返回 DB_S_ERRORSOCCURRED 尝试设置属性值。 *DwStatus*需要的 DBPROP 结构中的成员指示 DBPROPSTATUS_NOTSUPPORTED。|  
|DBPROP_INIT_LCID|SQL Server 的 OLE DB 驱动程序验证的区域设置 ID，并返回错误，如果区域设置 ID 不受支持或未安装在客户端上。|  
|DBPROP_INIT_LOCATION|SQL Server 的 OLE DB 驱动程序返回 DB_S_ERRORSOCCURRED 尝试设置属性值。 *DwStatus*需要的 DBPROP 结构中的成员指示 DBPROPSTATUS_NOTSUPPORTED。|  
|DBPROP_INIT_MODE|SQL Server 的 OLE DB 驱动程序返回 DB_S_ERRORSOCCURRED 尝试设置属性值。 *DwStatus*需要的 DBPROP 结构中的成员指示 DBPROPSTATUS_NOTSUPPORTED。|  
|DBPROP_INIT_PROMPT|SQL Server 的 OLE DB 驱动程序支持所有提示模式的数据源初始化。 SQL Server 的 OLE DB 驱动程序使用 DBPROMPT_NOPROMPT 作为其默认设置的属性。|  
|DBPROP_INIT_PROTECTION_LEVEL|SQL Server 的 OLE DB 驱动程序不支持连接到的实例上的保护级别[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。<br /><br /> SQL Server 的 OLE DB 驱动程序返回 DB_S_ERRORSOCCURRED 尝试设置属性值。 *DwStatus*需要的 DBPROP 结构中的成员指示 DBPROPSTATUS_NOTSUPPORTED。|  
|DBPROP_INIT_PROVIDERSTRING|请参阅本主题中后面的 SQL Server 字符串用于 OLE DB 驱动程序。|  
|DBPROP_INIT_TIMEOUT|SQL Server 的 OLE DB 驱动程序的实例的连接返回在初始化错误[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]无法建立在指定的秒数内。|  
  
 在提供程序特定属性集 dbpropset_sqlserverdbinit 限中，SQL Server 的 OLE DB 驱动程序定义这些附加的初始化属性。  
  
|属性 ID|Description|  
|-----------------|-----------------|  
|SSPROP_AUTH_OLD_PASSWORD|类型：VT_BSTR<br /><br /> R/W：写<br /><br /> 默认值：VT_EMPTY<br /><br /> 说明：当前或过期的密码。 有关详细信息，请参阅[更改密码以编程方式](../../oledb/features/changing-passwords-programmatically.md)。|  
|SSPROP_INIT_APPNAME|类型：VT_BSTR<br /><br /> 读/写︰ 读/写<br /><br /> 说明：客户端应用程序名称。|  
|SSPROP_INIT_AUTOTRANSLATE|类型：VT_BOOL<br /><br /> 读/写︰ 读/写<br /><br /> 默认值：VARIANT_TRUE<br /><br /> 说明：OEM/ANSI 字符转换。<br /><br /> VARIANT_TRUE: SQL Server 的 OLE DB 驱动程序将发送客户端和服务器之间的转换通过 Unicode 尽量减少客户端上的代码页和服务器之间的匹配扩展字符中的问题的 ANSI 字符字符串：<br /><br /> 客户端 DBTYPE_STR 数据发送到的实例[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **char**， **varchar**，或**文本**变量、 参数或列进行从字符转换为 Unicode 使用客户端的 ANSI 代码页 (ACP)，然后从 Unicode 字符使用服务器的 ACP 转换。<br /><br /> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]**char**， **varchar**，或**文本**数据发送到客户端 DBTYPE_STR 变量为从字符转换为 Unicode 使用 ACP 的服务器，然后从 Unicode 字符使用客户端 ACP 转换。<br /><br /> 这些转换为 SQL Server 执行客户端上通过 OLE DB 驱动程序。 这要求客户端上有在服务器上使用的同一 ACP。<br /><br /> 这些设置对于为下面这些传输而发生的转换无效：<br /><br /> Unicode DBTYPE_WSTR 客户端数据发送到**char**， **varchar**，或**文本**服务器上。<br /><br /> **char**， **varchar**，或**文本**服务器数据发送到客户端上的 Unicode DBTYPE_WSTR 变量。<br /><br /> ANSI DBTYPE_STR 客户端数据发送到 Unicode **nchar**， **nvarchar**，或**ntext**服务器上。<br /><br /> Unicode **char**， **varchar**，或**文本**服务器数据发送到客户端上的 ANSI DBTYPE_STR 变量。<br /><br /> VARIANT_FALSE: SQL Server 的 OLE DB 驱动程序不执行字符转换。<br /><br /> SQL Server 的 OLE DB 驱动程序不会转换发送到客户端 ANSI 字符 DBTYPE_STR 数据**char**， **varchar**，或**文本**变量、 参数或列上的服务器。 不执行任何转换上**char**， **varchar**，或**文本**从服务器发送到客户端上的 DBTYPE_STR 变量的数据。<br /><br /> 如果客户端和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例正在使用不同的 ACP，可能会错误地解释扩展字符。|  
|SSPROP_INIT_CURRENTLANGUAGE|类型：VT_BSTR<br /><br /> 读/写︰ 读/写<br /><br /> 说明：[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 语言名称。 标识用于系统消息选择和格式化的语言。 必须在运行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的计算机上安装该语言，否则数据源初始化将失败。|  
|SSPROP_INIT_DATATYPECOMPATIBILITY|类型：VT_UI2<br /><br /> 读/写︰ 读/写<br /><br /> 默认值： 0<br /><br /> 说明：在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 和 ActiveX 数据对象 (ADO) 应用程序之间实现数据类型兼容。 如果使用默认值 0，则数据类型处理将默认采用由访问接口使用的方案。 如果使用值 80，则数据类型处理仅使用 [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] 数据类型。 有关详细信息，请参阅[与 OLE DB 驱动程序的 SQL Server 使用 ADO](../../oledb/applications/using-ado-with-oledb-driver-for-sql-server.md)。|  
|SSPROP_INIT_ENCRYPT|类型：VT_BOOL<br /><br /> R/W：读/写<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明：若要加密通过网络传输的数据，应将 SSPROP_INIT_ENCRYPT 属性设置为 VARIANT_TRUE。<br /><br /> 如果打开了“启用协议加密”，则不论 SSPROP_INIT_ENCRYPT 如何设置，始终都会进行加密。 如果将它关闭，并将 SSPROP_INIT_ENCRYPT 设置为 VARIANT_TRUE，那么将进行加密。<br /><br /> 如果关闭“启用协议加密”，并将 SSPROP_INIT_ENCRYPT 设置为 VARIANT_FALSE，那么不进行加密。|  
|SSPROP_INIT_FAILOVERPARTNER|类型：VT_BSTR<br /><br /> 读/写︰ 读/写<br /><br /> 说明：指定用于数据库镜像的故障转移伙伴的名称。 它是初始化属性，并且只能在初始化之前设置。 在初始化之后，它将返回由主服务器返回的故障转移伙伴（如果有）。<br /><br /> 这允许智能应用程序缓存最新确定的备份服务器，但这样的应用程序应当知道，仅当初次建立（对于池连接则是重置）连接时该信息才会更新，因而在经过长时间的连接后可能会过时。<br /><br /> 建立连接之后，应用程序可以查询该属性，以确定故障转移伙伴的标识。 如果主服务器没有故障转移伙伴，则此属性将返回空字符串。 有关详细信息，请参阅[Using Database Mirroring](../../oledb/features/using-database-mirroring.md)。|  
|SSPROP_INIT_FILENAME|类型：VT_BSTR<br /><br /> 读/写︰ 读/写<br /><br /> 说明：指定可附加数据库的主文件名。 附加此数据库并使其成为连接的默认数据库。 若要使用 SSPROP_INIT_FILENAME，必须指定该数据库的名称作为初始化属性 DBPROP_INIT_CATALOG 的值。 如果该数据库名称不存在，它将查找在 SSPROP_INIT_FILENAME 中指定的主文件名，并使用在 DBPROP_INIT_CATALOG 中指定的名称来附加该数据库。 如果数据库是以前附加的，则 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 不重新附加它。|  
|SSPROP_INIT_MARSCONNECTION|类型：VT_BOOL<br /><br /> 读/写︰ 读/写<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明：指定是否对连接启用多个活动结果集 (MARS)。 必须在与数据库建立连接之前将该选项设置为 true。 有关详细信息，请参阅[使用多个活动结果集 &#40;MARS &#41;](../../oledb/features/using-multiple-active-result-sets-mars.md).|  
|SSPROP_INIT_NETWORKADDRESS|类型：VT_BSTR<br /><br /> 读/写︰ 读/写<br /><br /> 说明：运行由 DBPROP_INIT_DATASOURCE 属性指定的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的服务器的网络地址。|  
|SSPROP_INIT_NETWORKLIBRARY|类型：VT_BSTR<br /><br /> 读/写︰ 读/写<br /><br /> 说明：用于与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例通信的网络库 (DLL) 的名称。 该名称不应当包含路径或 .dll 文件扩展名。<br /><br /> 可以使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 客户端配置实用工具来自定义其默认值。<br /><br /> 注意： 只有 TCP 和 Named Pipes 支持此属性。 如果该属性在使用时带有前缀，最后将得到导致错误的双前缀，因为该属性用于在内部生成前缀。|  
|SSPROP_INIT_PACKETSIZE|类型：VT_I4<br /><br /> 读/写︰ 读/写<br /><br /> 说明：以字节为单位表示的网络数据包大小。 数据包大小属性值必须介于 512 和 32,767 之间。 默认值 OLE DB 驱动程序的 SQL Server 网络数据包大小为 4096。|  
|SSPROP_INIT_TAGCOLUMNCOLLATION|类型：BOOL<br /><br /> R/W：写<br /><br /> 默认值：FALSE<br /><br /> 说明：使用服务器端游标时，在数据库更新期间使用。 该属性用从服务器而不是客户端上的代码页获得的排序规则信息来标记数据。 当前，该属性仅供分布式查询进程使用，因为它知道目标数据的排序规则，并能正确转换它。|  
|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|类型：VT_BOOL<br /><br /> 读/写︰ 读/写<br /><br /> 默认值：VARIANT_FALSE<br /><br /> 说明：用于启用或禁用服务器证书验证。 该属性是读/写属性，但在已建立连接之后尝试设置它将导致错误。<br /><br /> 如果客户端配置为要求进行证书验证，则忽略该属性。 但是，应用程序可以将它与 SSPROP_INIT_ENCRYPT 一起使用，以保证即使将客户端配置为不要求加密，并且客户端上不提供证书，仍然会对应用程序与服务器之间的连接进行加密。<br /><br /> 客户端应用程序可以在打开连接后查询此属性，以确定使用的实际加密和验证设置。<br /><br /> 注意： 使用加密验证没有证书提供部分保护以防止探查数据包，但不能防止拦截的攻击。 它只是允许对发送到服务器的登录名和数据进行加密，而无需验证服务器证书。<br /><br /> 有关详细信息，请参阅[使用未经验证的加密](../../oledb/features/using-encryption-without-validation.md)。|  
|SSPROP_INIT_USEPROCFORPREP|类型：VT_I4<br /><br /> 读/写︰ 读/写<br /><br /> 默认值：SSPROPVAL_USEPROCFORPREP_ON<br /><br /> 说明：[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 存储过程的使用情况。 定义使用[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]临时存储过程以支持**ICommandPrepare**接口。 仅当连接到 SQL Server 6.5 时，该属性才有意义。 对于更高版本，将忽略该属性。<br /><br /> SSPROPVAL_USEPROCFORPREP_OFF：准备命令时，不创建临时存储过程。<br /><br /> SSPROPVAL_USEPROCFORPREP_ON：准备命令时，创建临时存储过程。 释放会话时，删除临时存储过程。<br /><br /> SSPROPVAL_USEPROCFORPREP_ON_DROP：准备命令时，创建临时存储过程。 该过程删除该命令后未准备好使用**ICommandPrepare::Unprepare**，当新的命令指定的命令对象**ICommandText::SetCommandText**，或何时发布到该命令的所有应用程序引用。|  
|SSPROP_INIT_WSID|类型：VT_BSTR<br /><br /> 读/写︰ 读/写<br /><br /> 说明：用于标识工作站的字符串。|  
  
 在提供程序特定属性集 DBPROPSET_SQLSERVERDATASOURCEINFO 中，SQL Server 的 OLE DB 驱动程序定义的其他属性;请参阅[数据源信息属性](../../oledb/ole-db-data-source-objects/data-source-information-properties.md)有关详细信息。  
  
## <a name="the-ole-db-driver-for-sql-server-string"></a>SQL Server 字符串 OLE DB 驱动程序  
 SQL Server 的 OLE DB 驱动程序识别在提供程序字符串属性值中的类似于 ODBC 的语法。 在建立与 OLE DB 数据源的连接时，访问接口字符串属性将作为 OLE DB 初始化属性 DBPROP_INIT_PROVIDERSTRING 的值提供。 该属性指定在实现与 OLE DB 数据源的连接时所需的特定于 OLE DB 访问接口的连接数据。 在字符串中，各元素是使用分号分隔的。 字符串中的最后一个元素必须以分号结束。 每个元素均由一个关键字、一个等号字符和在初始化时传递的值组成。 例如：  
  
```  
Server=MyServer;UID=MyUserName;  
```  
  
 使用 OLE DB 驱动程序的 SQL Server，使用者绝不会需要使用提供程序字符串属性。 使用者可以设置使用 OLE DB 或 OLE DB 驱动程序处理特定于 SQL Server 的初始化属性反射提供程序字符串中任何初始化属性。  
  
 SQL Server 的 OLE DB 驱动程序中可用的关键字的列表，请参阅[OLE DB 驱动程序的 SQL Server 连接字符串关键字](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)。  
  
## <a name="see-also"></a>另请参阅  
 [数据源对象 &#40; OLE DB &#41;](../../oledb/ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
