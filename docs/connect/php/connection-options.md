---
title: 连接选项 |Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6d1ea295-8e34-438e-8468-4bbc0f76192c
caps.latest.revision: 37
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 319ada38e07a30fa936608adce4e5c091ba098ec
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2018
ms.locfileid: "42783991"
---
# <a name="connection-options"></a>连接选项
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本主题列出了关联阵列中允许的选项（当在 SQLSRV 驱动程序中使用 [sqlsrv_connect](../../connect/php/sqlsrv-connect.md) 时）或数据源名称 (dsn) 中允许的关键字（当在PDO_SQLSRV 驱动程序中使用 [PDO::__construct](../../connect/php/pdo-construct.md) 时）。  

## <a name="table-of-connection-options"></a>表的连接选项
|Key|ReplTest1|描述|，则“默认”|  
|-------|---------|---------------|-----------|  
|APP|String|指定跟踪中所使用的应用程序名称。|未设置任何值。|  
|ApplicationIntent|String|连接到服务器时声明应用程序工作负荷类型。 可能的值为 ReadOnly 和 ReadWrite。<br /><br />有关详细信息[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]支持[!INCLUDE[ssHADR](../../includes/sshadr_md.md)]，请参阅[支持的高可用性和灾难恢复](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)。|ReadWrite|  
|AttachDBFileName|String|指定服务器应附加的数据库文件。|未设置任何值。|  
|身份验证|以下字符串之一：<br /><br />'SqlPassword'<br /><br />ActiveDirectoryPassword|指定的身份验证模式。|未设置。|  
|CharacterSet<br /><br />（在 PDO_SQLSRV 驱动程序中不受支持）|String|指定用于将数据发送到服务器的字符集。<br /><br />可能的值为 SQLSRV_ENC_CHAR 和 UTF-8。 有关详细信息，请参阅 [How to: Send and Retrieve UTF-8 Data Using Built-In UTF-8 Support](../../connect/php/how-to-send-and-retrieve-utf-8-data-using-built-in-utf-8-support.md)。|SQLSRV_ENC_CHAR|  
|ColumnEncryption|启用或禁用|指定是否启用始终加密功能。 |禁用|  
|ConnectionPooling|1 或 **true** ，表示启用连接池。<br /><br />0 或 **false** ，表示禁用连接池。|指定是否从连接池分配连接（1 或 true 表示是，0 或 false 表示否）<sup>1</sup>。|true (1)|  
|ConnectRetryCount|0 到 255 （含） 之间的整数|尝试重新建立断开的连接之前放弃的最大次数。 默认情况下进行一次尝试以重新建立连接时中断。 值为 0 表示将尝试任何重新连接。|@shouldalert|  
|ConnectRetryInterval|介于 1 和 60 （含） 之间的整数|以秒为单位，两次尝试重新建立的连接之间的时间。 应用程序将尝试在检测到断开的连接后立即重新连接，并会然后等到 ConnectRetryInterval 秒，然后重试。 如果 ConnectRetryCount 等于 0，则忽略此关键字。|@shouldalert|  
|“数据库”|String|指定用于建立连接的数据库名称<sup>2</sup>。|供登录时使用的默认数据库。|  
|驱动程序|String|指定用于与 SQL Server 进行通信的 Microsoft ODBC 驱动程序。<br /><br />可能的值有：<br />ODBC Driver 17 for SQL Server<br />ODBC Driver 13 for SQL Server<br />ODBC Driver 11 for SQL Server (仅 Windows)。|如果未指定 Driver 关键字，Microsoft Drivers for PHP for SQL Server 尝试查找受支持的 Microsoft ODBC 驱动程序在系统中，启动 ODBC 的最新版本，等等。|  
|Encrypt|1 或 **true** ，表示启用加密。<br /><br />0 或 **false** ，表示禁用加密。|指定是加密（1 或 true）还是解密（0 或 false）与 SQL Server 的通信<sup>3</sup>。|false (0)|  
|Failover_Partner|String|指定要在主服务器不可用时使用的服务器和数据库镜像的实例（如果已启用且已配置）。<br /><br />对于将 Failover_Partner 与 MultiSubnetFailover 结合使用，存在一些限制。 有关详细信息，请参阅[对高可用性和灾难恢复的支持](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)。|未设置任何值。|  
|keyStoreAuthentication|**KeyVaultPassword**<br /><br />**KeyVaultClientSecret**|用于访问 Azure 密钥保管库的身份验证方法。 控制何种凭据都与 KeyStorePrincipalId 和 KeyStoreSecret 一起使用。 有关详细信息，请参阅[使用 Azure Key Vault](../../connect/php/using-always-encrypted-php-drivers.md###using-azure-key-vault)。|未设置。|
|KeyStorePrincipalId|String|查找 Azure 密钥保管库的访问的帐户标识符。 <br /><br />如果 KeyStoreAuthentication **KeyVaultPassword**，这必须是 Azure Active Directory 用户名。 <br /><br />如果 KeyStoreAuthentication **KeyVaultClientSecret**，这必须是应用程序客户端 id。|未设置。|
|keyStoreSecret|String|查找 Azure 密钥保管库的访问的帐户的凭据密码。 <br /><br />如果 KeyStoreAuthentication **KeyVaultPassword**，它必须是 Azure Active Directory 密码。 <br /><br />如果 KeyStoreAuthentication **KeyVaultClientSecret**，这必须是应用程序客户端密码。|未设置。|
|LoginTimeout|整数（SQLSRV 驱动程序）<br /><br />字符串（PDO_SQLSRV 驱动程序）|指定在连接尝试失败前等待的秒数。|无超时。|  
|MultipleActiveResultSets|1 或 **true** ，表示使用多个活动的结果集。<br /><br />0 或 **false** ，表示禁用多个活动的结果集。|禁用或显式启用对多个活动的结果集 (MARS) 的支持。<br /><br />有关详细信息，请参阅[如何：禁用多个活动结果集 (MARS)](../../connect/php/how-to-disable-multiple-active-resultsets-mars.md)。|true (1)|  
|MultiSubnetFailover|String|在连接到 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 可用性组或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 故障转移群集实例的可用性组侦听程序时，应始终指定 multiSubnetFailover=yes。 multiSubnetFailover=yes 将配置 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 以便更快地检测和连接到（当前）活动服务器。 可能的值为 Yes 和 No。<br /><br />有关详细信息[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]支持[!INCLUDE[ssHADR](../../includes/sshadr_md.md)]，请参阅[支持的高可用性和灾难恢复](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)。|否|  
|PWD<br /><br />（在 PDO_SQLSRV 驱动程序中不受支持）|String|指定与使用 SQL Server 身份验证进行连接时使用的用户 ID 关联的密码<sup>4</sup>。|未设置任何值。|  
|QuotedId|1 或 true，表示使用 SQL-92 规则。<br /><br />0 或 **false** ，表示使用旧规则。|指定对带引号的标识符是使用 SQL-92 规则（1 或 true）还是使用旧的 Transact-SQL 规则（0 或 false）。|true (1)|  
|ReturnDatesAsStrings<br /><br />（在 PDO_SQLSRV 驱动程序中不受支持）|1 或 **true** ，表示以字符串的形式返回日期和时间类型。<br /><br />0 或 **false** ，表示以 PHP **DateTime** 的形式返回日期和时间类型。|以字符串或 PHP 类型的形式检索日期和时间类型（datetime、date、time、datetime2 和 datetimeoffset）。 当使用 PDO_SQLSRV 驱动程序时，日期将以字符串的形式返回。 PDO_SQLSRV 驱动程序不包含 datetime 类型。<br /><br />有关详细信息，请参阅 [如何：使用 SQLSRV 驱动程序以字符串的形式检索日期和时间类型](../../connect/php/how-to-retrieve-date-and-time-type-as-strings-using-the-sqlsrv-driver.md)。|**false**|  
|可滚动|String|“缓冲”表示你希望使用客户端（缓冲）游标，这将允许你将整个结果集缓存到内存。 有关详细信息，请参阅[游标类型（SQLSRV 驱动程序）](../../connect/php/cursor-types-sqlsrv-driver.md)。|只进游标|  
|“服务器”<br /><br />（在 SQLSRV 驱动程序中不受支持）|String|要连接到的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。<br /><br />你还可以指定要连接到 AlwaysOn 可用性组的虚拟网络名称。 有关详细信息[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]支持[!INCLUDE[ssHADR](../../includes/sshadr_md.md)]，请参阅[支持的高可用性和灾难恢复](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)。|Server 是必需的关键字（尽管它不必是连接字符串中的第一个关键字）。 如果服务器名称未传递给该关键字，将尝试连接到本地实例。<br /><br />传递给 Server 的值可以是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的名称，也可以是该实例的 IP 地址。 你可以选择指定一个端口号（例如 `sqlsrv:server=(local),1033`）。<br /><br />从 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 的版本 3.0 开始，你还可以指定带有 `server=(localdb)\instancename`的 LocalDB 实例。 有关详细信息，请参阅[对 LocalDB 的支持](../../connect/php/php-driver-for-sql-server-support-for-localdb.md)。|  
|TraceFile|String|指定用于跟踪数据的文件的路径。|未设置任何值。|  
|TraceOn|1 或 **true** ，表示启用跟踪。<br /><br />0 或 **false** ，表示禁用跟踪。|指定对正在建立的连接是启用（1 或 true）还是禁用（0 或 false）ODBC 跟踪。|false (0)|  
|TransactionIsolation|SQLSRV 驱动程序使用以下值：<br /><br />SQLSRV_TXN_READ_UNCOMMITTED<br /><br />SQLSRV_TXN_READ_COMMITTED<br /><br />SQLSRV_TXN_REPEATABLE_READ<br /><br />SQLSRV_TXN_SNAPSHOT<br /><br />SQLSRV_TXN_SERIALIZABLE<br /><br />PDO_SQLSRV 驱动程序使用以下值：<br /><br />PDO::SQLSRV_TXN_READ_UNCOMMITTED<br /><br />PDO::SQLSRV_TXN_READ_COMMITTED<br /><br />PDO::SQLSRV_TXN_REPEATABLE_READ<br /><br />PDO::SQLSRV_TXN_SNAPSHOT<br /><br />PDO::SQLSRV_TXN_SERIALIZABLE|指定事务隔离级别。<br /><br />有关事务隔离的详细信息，请参阅 SQL Server 文档中的 [设置事务隔离级别](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)。|SQLSRV_TXN_READ_COMMITTED<br /><br />或多个<br /><br />PDO::SQLSRV_TXN_READ_COMMITTED|  
|transparentNetworkIPResolution|启用或禁用|影响的主机名相关联的连接顺序时第一个解析主机名的 IP 不响应，并且有多个 Ip。<br /><br />它与 MultiSubnetFailover 提供不同的连接序列进行交互。 有关详细信息，请参阅[透明网络 IP 解析](../../connect/php/php-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)或[使用透明网络 IP 解析](https://docs.microsoft.com/sql/connect/odbc/using-transparent-network-ip-resolution)。|已启用|
|TrustServerCertificate|1 或 **true** ，表示信任证书。<br /><br />0 或 **false** ，表示不信任证书。|指定客户端是应信任（1 或 true）还是应拒绝（0 或 false）自签名的服务器证书。|false (0)|  
|UID<br /><br />（在 PDO_SQLSRV 驱动程序中不受支持）|String|指定在使用 SQL Server 身份验证进行连接时要使用的用户 ID<sup>4</sup>。|未设置任何值。|  
|WSID|String|指定用于跟踪的计算机的名称。|未设置任何值。|  

1. `ConnectionPooling`属性不能用于启用/禁用连接池在 Linux 和 mac。 请参阅[连接池 (Microsoft Drivers for PHP for SQL Server)](../../connect/php/connection-pooling-microsoft-drivers-for-php-for-sql-server.md)。

2. 在已建立连接上执行的所有查询都会针对 Database 属性所指定的数据库进行。 不过，如果用户具有相应权限，则可以使用完全限定的名称访问其他数据库中的数据。 例如，如果使用 Database 连接属性设置 master 数据库，则仍可以使用完全限定的名称执行可访问 AdventureWorks.HumanResources.Employee 表格的 Transact-SQL 查询。  

3. 因为加密数据需要计算开销，所以启用 *Encryption* 可能会影响某些应用程序的性能。  

4. 要连接到的 *UID* 身份验证进行连接时，必须同时设置 *PWD* 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 属性。  

许多支持的键都是 ODBC 连接字符串属性。 有关 ODBC 连接字符串的信息，请参阅 [将连接字符串关键字用于 SQL Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)。

## <a name="see-also"></a>另请参阅  
[连接到服务器](../../connect/php/connecting-to-the-server.md)  
