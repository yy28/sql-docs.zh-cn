---
title: "以编程方式更改密码 |Microsoft 文档"
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
- data access [SQL Server Native Client], password expiration
- SQL Server Native Client ODBC driver, passwords
- SQL Server Native Client OLE DB provider, passwords
- passwords [SQL Server], expiration
- SQLNCLI, password expiration
- expiration [SQL Server Native Client]
- passwords [SQL Server], modifying
- expired passwords [SQL Server Native Client]
- SQL Server Native Client, password expiration
- modifying passwords
ms.assetid: 624ad949-5fed-4ce5-b319-878549f9487b
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bb5e1dbff4a9a528690ff3172da2329ae9a5c28e
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="changing-passwords-programmatically"></a>以编程方式更改密码
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  在 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 之前，如果用户的密码过期，则只有管理员能对其进行重置。 开头[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]处理以编程方式通过密码过期的本机客户端支持[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序和[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序，并通过对更改**SQL Server 登录名**对话框。  
  
> [!NOTE]  
>  如果可能，请在运行时提示用户输入他们的凭据，并避免用持久化格式存储他们的凭据。 如果您必须保留其凭据，则应加密它们使用[Win32 加密 API](http://go.microsoft.com/fwlink/?LinkId=64532)。 有关使用密码的详细信息，请参阅[强密码](../../../relational-databases/security/strong-passwords.md)。  
  
## <a name="sql-server-login-error-codes"></a>SQL Server 登录错误代码  
 当由于身份验证问题而导致无法连接时，以下 SQL Server 错误代码之一可供应用程序使用，以帮助诊断和恢复。  
  
|SQL Server 错误代码|错误消息|  
|---------------------------|-------------------|  
|15113|用户 '%.*ls' 登录失败。原因: 密码验证失败。 帐户已锁定。|  
|18463|用户 "%.*ls" 登录失败。 原因: 密码更改失败。 此时无法使用密码。|  
|18464|用户 "%.*ls" 登录失败。 原因: 密码更改失败。 该密码太短，不符合策略要求。|  
|18465|用户 "%.*ls" 登录失败。 原因: 密码更改失败。 密码太长，不符合策略要求。|  
|18466|用户 "%.*ls" 登录失败。 原因: 密码更改失败。 该密码不够复杂，不符合策略要求。|  
|18467|用户 "%.*ls" 登录失败。 原因: 密码更改失败。 该密码不符合密码筛选器 DLL 的要求。|  
|18468|用户 "%.*ls" 登录失败。 原因: 密码更改失败。 在密码验证过程中出错。|  
|18487|用户 "%.*ls" 登录失败。 原因: 该帐户的密码已过期。|  
|18488|用户 "%.*ls" 登录失败。 原因: 该帐户的密码必须更改。|  
  
## <a name="sql-server-native-client-ole-db-provider"></a>SQL Server Native Client OLE DB 访问接口  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序支持密码过期，但用户界面并以编程方式。  
  
### <a name="ole-db-user-interface-password-expiration"></a>OLE DB 用户界面密码过期  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序支持通过对所做更改的密码过期**SQL Server 登录名**对话框。 如果将 DBPROP_INIT_PROMPT 的值设置为 DBPROMPT_NOPROMPT，则在密码已过期的情况下初始连接尝试将失败。  
  
 如果 DBPROP_INIT_PROMPT 已设置为任何其他值，用户将看到**SQL Server 登录名**对话框中，而不考虑是否的密码已过期。 用户可以单击**选项**按钮，然后检查**更改密码**更改密码。  
  
 如果用户单击确定，并且密码已过期，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]提示用户输入并确认新密码使用**更改 SQL Server 密码**对话框。  
  
#### <a name="ole-db-prompt-behavior-and-locked-accounts"></a>OLE DB 提示行为和锁定的帐户  
 连接尝试可能会由于帐户被锁定而失败。 如果发生这种情况的显示以下**SQL Server 登录名**对话框中，向用户显示服务器错误消息并中止连接尝试。 此外，它也可能出现以下的显示**更改 SQL Server 密码**对话框，如果用户可为旧密码输入错误值。 在这种情况下，将显示相同的错误消息，并且连接尝试将中止。  
  
#### <a name="ole-db-connection-pooling-password-expiration-and-locked-accounts"></a>OLE DB 连接池、密码过期和锁定的帐户  
 当连接在连接池中仍处于活动状态时，帐户可能被锁定或其密码可能已过期。 服务器会在以下两种情况下检查密码是否已过期以及帐户是否已锁定。 第一种情况是首次创建连接时。 第二种情况是从相应池中获取相应连接以重置连接时。  
  
 如果重置尝试失败，则将从相应池中删除相应连接且返回一个错误。  
  
### <a name="ole-db-programmatic-password-expiration"></a>OLE DB 编程密码过期  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序支持通过添加已添加到 dbpropset_sqlserverdbinit 限属性集 SSPROP_AUTH_OLD_PASSWORD （类型 VT_BSTR） 属性的密码过期。  
  
 现有“密码”属性是指 DBPROP_AUTH_PASSWORD，用于存储新密码。  
  
> [!NOTE]  
>  在连接字符串中，“旧密码”属性会设置 SSPROP_AUTH_OLD_PASSWORD，它是当前（有可能是过期的）密码，通过提供程序字符串属性无法得到该密码。  
  
 访问接口不保留此属性的值。 如果设置此属性，则访问接口不使用连接池进行首次连接，原因是将进行新连接。 如果密码更改成功，则不能重新使用当前连接，原因是当前连接仍包含旧密码，这些密码在密码更改后失效。 此外，如果登录成功，则访问接口将清除此属性。 如果随后尝试检索旧密码，则将返回 VT_EMPTY。  
  
> [!NOTE]  
>  不得保留 SSPROP_AUTH_OLD_PASSWORD，因为只有在密码过期时才使用它。  
  
 请注意，只要设置“旧密码”属性，访问接口就会假定正在尝试更改密码，除非还指定了 Windows 身份验证，这种情况下 Windows 身份验证始终优先。  
  
 如果使用 Windows 身份验证，则指定旧密码会导致 DB_E_ERRORSOCCURRED 或 DB_S_ERRORSOCCURRED 具体取决于是否旧密码指定为必需或可选分别和 DBPROPSTATUS_ 的状态值在中返回 CONFLICTINGBADVALUE *dwStatus*。 检测到此时**idbinitialize:: Initialize**调用。  
  
 如果更改密码的尝试意外失败，则服务器将返回错误代码 18468。 将从连接尝试返回标准的 OLEDB 错误。  
  
 有关 dbpropset_sqlserverdbinit 限属性集的详细信息，请参阅[初始化和授权属性](../../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md)。  
  
## <a name="sql-server-native-client-odbc-driver"></a>SQL Server Native Client ODBC 驱动程序  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序支持密码过期，但用户界面并以编程方式。  
  
### <a name="odbc-user-interface-password-expiration"></a>ODBC 用户界面密码过期  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序还支持通过对所做更改的密码过期**SQL Server 登录名**对话框。  
  
 如果[SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md)称为和的值**DriverCompletion**如果密码已过期设置为 SQL_DRIVER_NOPROMPT，则初始连接尝试将失败。 通过后续调用返回的 SQLSTATE 值 28000 和本机错误代码值 18487 **SQLError**或**SQLGetDiagRec**。  
  
 如果**DriverCompletion**已设置为任何其他值，则用户将看到**SQL Server 登录名**对话框中，而不考虑是否的密码已过期。 用户可以单击**选项**按钮，然后检查**更改密码**更改密码。  
  
 如果用户单击确定，并且密码已过期，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]提示输入并确认新密码使用**更改 SQL Server 密码**对话框。  
  
#### <a name="odbc-prompt-behavior-and-locked-accounts"></a>ODBC 提示行为和锁定的帐户  
 连接尝试可能会由于帐户被锁定而失败。 如果发生这种情况的显示以下**SQL Server 登录名**对话框中，向用户显示服务器错误消息并中止连接尝试。 此外，它也可能出现以下的显示**更改 SQL Server 密码**对话框，如果用户可为旧密码输入错误值。 在这种情况下，将显示相同的错误消息，并且连接尝试将中止。  
  
#### <a name="odbc-connection-pooling-password-expiry-and-locked-accounts"></a>ODBC 连接池、密码过期和锁定的帐户  
 当连接在连接池中仍处于活动状态时，帐户可能被锁定或其密码可能已过期。 服务器会在以下两种情况下检查密码是否已过期以及帐户是否已锁定。 第一种情况是首次创建连接时。 第二种情况是从相应池中获取相应连接以重置连接时。  
  
 如果重置尝试失败，则将从相应池中删除相应连接且返回一个错误。  
  
### <a name="odbc-programmatic-password-expiration"></a>ODBC 编程密码过期  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序还支持通过在添加 SQL_COPT_SS_OLDPWD 属性在连接到服务器使用之前设置密码过期[SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)函数。  
  
 连接句柄的 SQL_COPT_SS_OLDPWD 属性是指已过期的密码。 对于此属性，没有连接字符串属性，原因是如果有的话会影响连接池。 如果登录成功，则驱动程序将清除此属性。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序，对此功能的四个情况下均返回 SQL_ERROR： 密码过期、 密码策略冲突、 帐户锁定，并且旧的密码属性时使用 Windows 身份验证的设置时。 该驱动程序向用户返回相应的错误消息时[SQLGetDiagField](../../../relational-databases/native-client-odbc-api/sqlgetdiagfield.md)调用。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Native Client 功能](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
