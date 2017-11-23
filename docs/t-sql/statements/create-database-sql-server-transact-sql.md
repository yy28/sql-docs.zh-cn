---
title: "创建数据库 (SQL Server TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DATABASE_TSQL
- DATABASE
- CONTAINMENT_TSQL
- CREATE DATABASE
- CREATE_DATABASE_TSQL
- CONTAINS_FILESTREAM_TSQL
- CONTAINS FILESTREAM
- CONTAINMENT
dev_langs: TSQL
helpviewer_keywords:
- snapshots [SQL Server database snapshots], creating
- databases [SQL Server], creating
- model database [SQL Server], database creation
- mounted drives [SQL Server]
- CREATE DATABASE
- CREATE DATABASE statement
- file creation [SQL Server]
- creating databases
- containment
- filegroups [SQL Server], database creation
- database creation [SQL Server], CREATE DATABASE statement
- moving databases
- attaching databases [SQL Server], CREATE DATABASE...FOR ATTACH
ms.assetid: 29ddac46-7a0f-4151-bd94-75c1908c89f8
caps.latest.revision: "212"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 57fe9fffdb553dffc3cd019d36692a8c34681817
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="create-database-sql-server-transact-sql"></a>CREATE DATABASE (SQL Server Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  创建一个新数据库及存储该数据库、数据库快照的文件，或从先前创建的数据库的已分离文件中附加数据库。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
      Create a database  
CREATE DATABASE database_name   
[ CONTAINMENT = { NONE | PARTIAL } ]  
[ ON   
      [ PRIMARY ] <filespec> [ ,...n ]   
      [ , <filegroup> [ ,...n ] ]   
      [ LOG ON <filespec> [ ,...n ] ]   
]   
[ COLLATE collation_name ]  
[ WITH  <option> [,...n ] ]  
[;]  
  
<option> ::=  
{  
      FILESTREAM ( <filestream_option> [,...n ] )  
    | DEFAULT_FULLTEXT_LANGUAGE = { lcid | language_name | language_alias }  
    | DEFAULT_LANGUAGE = { lcid | language_name | language_alias }  
    | NESTED_TRIGGERS = { OFF | ON }  
    | TRANSFORM_NOISE_WORDS = { OFF | ON}  
    | TWO_DIGIT_YEAR_CUTOFF = <two_digit_year_cutoff>   
    | DB_CHAINING { OFF | ON }  
    | TRUSTWORTHY { OFF | ON }  
}  
  
<filestream_option> ::=  
{  
      NON_TRANSACTED_ACCESS = { OFF | READ_ONLY | FULL }  
    | DIRECTORY_NAME = 'directory_name'   
}  
  
<filespec> ::=   
{  
(  
    NAME = logical_file_name ,  
    FILENAME = { 'os_file_name' | 'filestream_path' }   
    [ , SIZE = size [ KB | MB | GB | TB ] ]   
    [ , MAXSIZE = { max_size [ KB | MB | GB | TB ] | UNLIMITED } ]   
    [ , FILEGROWTH = growth_increment [ KB | MB | GB | TB | % ] ]  
)  
}  
  
<filegroup> ::=   
{  
FILEGROUP filegroup name [ [ CONTAINS FILESTREAM ] [ DEFAULT ] | CONTAINS MEMORY_OPTIMIZED_DATA ]  
    <filespec> [ ,...n ]  
}  
  
<service_broker_option> ::=  
{  
    ENABLE_BROKER  
  | NEW_BROKER  
  | ERROR_BROKER_CONVERSATIONS  
}  
  
```  
  
```  
  
      Attach a database  
CREATE DATABASE database_name   
    ON <filespec> [ ,...n ]   
    FOR { { ATTACH [ WITH <attach_database_option> [ , ...n ] ] }  
        | ATTACH_REBUILD_LOG }  
[;]  
  
<attach_database_option> ::=  
{  
      <service_broker_option>  
    | RESTRICTED_USER  
    | FILESTREAM ( DIRECTORY_NAME = { 'directory_name' | NULL } )  
}  
  
```  
  
```  
  
      Create a database snapshot  
CREATE DATABASE database_snapshot_name   
    ON   
    (  
        NAME = logical_file_name,  
        FILENAME = 'os_file_name'   
    ) [ ,...n ]   
    AS SNAPSHOT OF source_database_name  
[;]  
```  
  
## <a name="arguments"></a>参数  
 *database_name*  
 为新数据库的名称。 数据库名称必须是唯一的实例内[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]并遵守的规则[标识符](../../relational-databases/databases/database-identifiers.md)。  
  
 *database_name*最多可包含 128 个字符，除非日志文件未指定逻辑名称。 如果未指定逻辑日志文件名称，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]生成*logical_file_name*和*os_file_name*通过追加后缀日志*database_name*. 这就限制了*database_name*到 123 个字符，以生成的逻辑文件名为不能超过 128 个字符。  
  
 如果未指定数据文件名称，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用*database_name*为这两者*logical_file_name*并将它作为*os_file_name*。 默认路径从注册表中获得。 可以使用更改的默认路径**服务器属性 （数据库设置页）**中[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。 更改默认路径要求重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 CONTAINMENT = { NONE | PARTIAL }  

**适用于**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 指定数据库的包含状态。 NONE = 非包含数据库。 PARTIAL = 部分包含的数据库。  
  
 ON  
 指定显式定义用来存储数据库数据部分的磁盘文件（数据文件）。 跟一个逗号分隔的列表时需要 ON \<filespec > 定义主文件组的数据文件的项。 主文件组中的文件列表可以跟可选、 以逗号分隔的列表\<文件组 > 定义用户文件组和其文件的项。  
  
 PRIMARY  
 指定关联\<filespec > 列表定义的主文件。 中指定的第一个文件\<filespec > 主文件组中的项将成为主文件。 一个数据库只能有一个主文件。 有关详细信息，请参阅 [Database Files and Filegroups](../../relational-databases/databases/database-files-and-filegroups.md)。  
  
 如果没有指定 PRIMARY，那么 CREATE DATABASE 语句中列出的第一个文件将成为主文件。  
  
 LOG ON  
 指定显式定义用来存储数据库日志的磁盘文件（日志文件）。 LOG ON 后跟一个逗号分隔的列表\<filespec > 定义的日志文件的项。 如果未指定 LOG ON，自动创建一个日志文件，具有是为数据库或 512 KB 的所有数据文件的大小之和的 25%的大小，大者为准。 此文件放置于默认的日志文件位置。 有关此位置的信息，请参阅[查看或更改默认位置获得数据和日志文件 &#40;SQL Server Management Studio &#41;](../../database-engine/configure-windows/view-or-change-the-default-locations-for-data-and-log-files.md).  
  
 不能对数据库快照指定 LOG ON。  
  
 COLLATE *collation_name*  
 指定数据库的默认排序规则。 排序规则名称既可以是 Windows 排序规则名称，也可以是 SQL 排序规则名称。 如果没有指定排序规则，则将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的默认排序规则分配为数据库的排序规则。 不能对数据库快照指定排序规则名称。  
  
 不能使用 FOR ATTACH 或 FOR ATTACH_REBUILD_LOG 子句指定排序规则名称。 有关如何更改附加的数据库的排序规则的信息，请访问此[Microsoft Web 站点](http://go.microsoft.com/fwlink/?linkid=16419&kbid=325335)。  
  
 有关 Windows 和 SQL 排序规则名称的详细信息，请参阅[COLLATE &#40;Transact SQL &#41;](~/t-sql/statements/collations.md).  
  
> [!NOTE]  
>  包含数据库的排序方式不同于非包含数据库。 请参阅[Contained Database Collations](../../relational-databases/databases/contained-database-collations.md)有关详细信息。  
  
 与\<选项 >  
 -   **\<filestream_options >** 
  
     NON_TRANSACTED_ACCESS = { **OFF** |READ_ONLY |完整}  
**适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。
  
     指定对数据库的非事务性 FILESTREAM 访问的级别。  
  
    |值|说明|  
    |-----------|-----------------|  
    |OFF|禁用非事务性访问。|  
    |READONLY|可以通过非事务性进程读取此数据库中的 FILESTREAM 数据。|  
    |FULL|启用对 FILESTREAM FileTable 的完全非事务性访问。|  
  
     DIRECTORY_NAME = \<directory_name >**适用于**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
     与 Windows 兼容的目录名称。 此名称应在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的所有 Database_Directory 名称中唯一。 无论 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 排序规则设置如何，唯一性比较都不区分大小写。 在此数据库中创建 FileTable 之前，应设置此选项。  
  
 仅在将 CONTAINMENT 设置为 PARTIAL 之后，才允许使用以下选项。 如果将 CONTAINMENT 设置为 NONE，将发生错误。  
  
-   **DEFAULT_FULLTEXT_LANGUAGE = \<lcid > |\<语言名称 > |\<语言别名 >**  
  
**适用于**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
     See [Configure the default full-text language Server Configuration Option](../../database-engine/configure-windows/configure-the-default-full-text-language-server-configuration-option.md) for a full description of this option.  
  
-   **DEFAULT_LANGUAGE = \<lcid > |\<语言名称 > |\<语言别名 >**  
  
**适用于**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
     See [Configure the default language Server Configuration Option](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md) for a full description of this option.  
  
-   **NESTED_TRIGGERS = {OFF |ON}**  
  
**适用于**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
     See [Configure the nested triggers Server Configuration Option](../../database-engine/configure-windows/configure-the-nested-triggers-server-configuration-option.md) for a full description of this option.  
  
-   **TRANSFORM_NOISE_WORDS = {OFF |ON}**  
  
**适用于**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
     See [transform noise words Server Configuration Option](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md)for a full description of this option.  
  
-   **TWO_DIGIT_YEAR_CUTOFF = {2049年 |\<1753年到 9999 之间的任何年 >}**  
  
     表示一年的四位。 2049 为默认值。 请参阅[配置两位数年份截止服务器配置选项](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md)有关此选项的完整说明。  
  
-   **DB_CHAINING {OFF |ON}**  
  
     当指定为 ON 时，数据库可以为跨数据库所有权链的源或目标。  
  
     当为 OFF 时，数据库不能参与跨数据库所有权链接。 默认为 OFF。  
  
    > [!IMPORTANT]  
    >  如果 cross db ownership chaining 服务器选项为 0 (OFF)，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例将可以识别此设置。 如果 cross db ownership chaining 为 1 (ON)，则不论此选项为何值，所有用户数据库都可以参与跨数据库所有权链。 此选项通过设置[sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)。  
  
     若要设置此选项，要求具有 sysadmin 固定服务器角色的成员身份。 无法在这些系统数据库上设置 DB_CHAINING 选项： master、 model、 tempdb。  
  
-   **可信 {OFF |ON}**  
  
     当指定 ON 时，使用模拟上下文的数据库模块（例如，视图、用户定义函数或存储过程）可以访问数据库以外的资源。  
  
     当为 OFF 时，模拟上下文中的数据库模块不能访问数据库以外的资源。 默认为 OFF。  
  
     只要附加数据库，TRUSTWORTHY 就会设置为 OFF。  
  
     默认情况下，除 msdb 数据库之外的所有系统数据库都将 TRUSTWORTHY 设置为 OFF。 对于 model 和 tempdb 数据库，不能更改此值。 建议在任何情况下都不要将 master 数据库的 TRUSTWORTHY 选项设置为 ON。  
  
     若要设置此选项，要求具有 sysadmin 固定服务器角色的成员身份。  
  
 FOR ATTACH [WITH \< attach_database_option >] 通过创建了数据库的指定[附加](../../relational-databases/databases/database-detach-and-attach-sql-server.md)一组现有的操作系统文件。 必须有\<filespec > 指定的主文件的条目。 唯一其他\<filespec > 所需的条目是指拥有受第一个数据库时的不同路径的任何文件创建或上次附加。 A \<filespec > 条目必须指定对于这些文件。  
  
 FOR ATTACH 具有以下要求：  
  
-   所有数据文件（MDF 和 NDF）都必须可用。  
  
-   如果存在多个日志文件，这些文件都必须可用。  
  
 如果一个可读/写数据库具有一个当前不可用的日志文件，并且进行附加操作前在没有使用用户或打开的事务的情况下关闭了该数据库，那么 FOR ATTACH 会自动重新生成日志文件并更新主文件。 相比之下，对于只读数据库，由于主文件不能更新，将不能重新生成日志。 因此，当你附加的日志不可用的只读数据库，你必须提供日志文件中或 FOR ATTACH 子句中的文件。  
  
> [!NOTE]  
>  无法在早期版本的 SQL Server 中附加由较新版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 创建的数据库。  
  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，作为待附加数据库的组成部分的所有全文文件也将随之一起附加。 若要指定全文目录的新路径，请指定不带全文操作系统文件名的新位置。 有关详细信息，请参阅“示例”部分。  
  
 附加数据库将包含"目录名称"的 FILESTREAM 选项的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例将提示[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以验证 Database_Directory 名称是否唯一。 如果不是这样，则附加操作将失败并出现错误，"FILESTREAM Database_Directory 名称\<名称 > 不是此 SQL Server 实例中唯一的"。 若要避免此错误，可选参数， *directory_name*，应在传递给此操作。  
  
 不能对数据库快照指定 FOR ATTACH。  
  
 对于 ATTACH，可以指定 RESTRICTED_USER 选项。 RESTRICTED_USER 只允许 db_owner 固定数据库角色成员以及 dbcreator 和 sysadmin 固定服务器角色成员连接到数据库，不过对连接数没有限制。 无资格用户的尝试将被拒绝。  
  
 如果数据库使用[!INCLUDE[ssSB](../../includes/sssb-md.md)]，使用 WITH \<service_broker_option > 在 FOR ATTACH 语句中： 
  
 \<service_broker_option > 控件[!INCLUDE[ssSB](../../includes/sssb-md.md)]消息传递和[!INCLUDE[ssSB](../../includes/sssb-md.md)]数据库标识符。 仅当使用 FOR ATTACH 子句时，才能指定 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 选项。  
  
 ENABLE_BROKER  
 指定对指定的数据库启用 [!INCLUDE[ssSB](../../includes/sssb-md.md)]。 也就是说，将启动消息传递，并且 is_broker_enabled 设置为 true sys.databases 目录视图中。 数据库保留现有的 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 标识符。  
  
 NEW_BROKER  
 在 sys.databases 和还原数据库中都创建一个新的 service_broker_guid 值，并通过清除结束所有会话端点。 Broker 已启用，但未向远程会话端点发送消息。 必须使用新标识符重新创建任何引用旧 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 标识符的路由。  
  
 ERROR_BROKER_CONVERSATIONS  
 结束所有会话，并产生一个错误指出数据库已附加或还原。 Broker 一直处于禁用状态直到此操作完成，然后再将其启用。 数据库保留现有的 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 标识符。  
  
 当您附加已复制的数据库而不是分离的数据库时，请注意以下事项：  
  
-   如果将数据库附加到与原始数据库相同的服务器实例和版本，则不需要执行其他步骤。  
  
-   如果将数据库附加到同一个服务器实例，但你必须执行的升级版本[sp_vupgrade_replication](../../relational-databases/system-stored-procedures/sp-vupgrade-replication-transact-sql.md)之后附加操作已完成升级复制。  
  
-   如果将数据库附加到不同的服务器实例，无论何种版本，则必须执行[sp_removedbreplication](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md)附加操作完成后删除复制。  
  
> [!NOTE]  
>  附加使用**vardecimal**存储格式，但[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]必须至少升级到[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]Service Pack 2。 无法将使用 Vardecimal 存储格式的数据库附加到早期版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 有关详细信息**vardecimal**存储格式，请参阅[数据压缩](../../relational-databases/data-compression/data-compression.md)。  
  
 当数据库第一次附加或还原到新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例时，数据库主密钥（由服务主密钥加密）的副本尚未存储在服务器中。 必须使用 **OPEN MASTER KEY** 语句解密数据库主密钥 (DMK)。 一旦 DMK 解密后，通过使用 **ALTER MASTER KEY REGENERATE** 语句向服务器提供 DMK（使用服务主密钥 (SMK) 加密）的副本，即可拥有将来启用自动解密的选项。 当数据库已从较早版本升级后，应重新生成 DMK 以使用更新的 AES 算法。 有关重新生成 DMK 的详细信息，请参阅 [ALTER MASTER KEY (Transact-SQL)](../../t-sql/statements/alter-master-key-transact-sql.md)。 重新生成 DMK 密钥以升级到 AES 所需的时间取决于 DMK 保护的对象数。 重新生成 DMK 密钥以升级到 AES 只在必需时执行一次，不影响将来作为密钥循环策略的一部分而重新生成的过程。 有关如何通过使用升级数据库的信息将附加，请参阅[升级数据库使用分离和附加 &#40;Transact SQL &#41;](../../relational-databases/databases/upgrade-a-database-using-detach-and-attach-transact-sql.md).  
  
 **安全说明**建议请不要从未知或不受信任的源附加数据库。 此类数据库可能包含恶意代码，这些代码可能会执行非预期的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 代码，或者通过修改架构或物理数据库结构导致错误。 在使用来自未知或不受信任源的数据库之前，运行[DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)的数据库上的非生产服务器，然后检查的代码，例如存储的过程或其他用户定义的代码，在数据库中。  
  
> [!NOTE]  
>  **TRUSTWORTHY**和**DB_CHAINING**选项附加数据库时有任何影响。  
  
 FOR ATTACH_REBUILD_LOG  
 指定通过附加一组现有的操作系统文件来创建数据库。 该选项只限于读/写数据库。 必须有 *\<filespec >*指定主文件项。 如果缺少一个或多个事务日志文件，将重新生成日志文件。 ATTACH_REBUILD_LOG 自动创建一个新的 1 MB 的日志文件。 此文件放置于默认的日志文件位置。 有关此位置的信息，请参阅[查看或更改默认位置获得数据和日志文件 &#40;SQL Server Management Studio &#41;](../../database-engine/configure-windows/view-or-change-the-default-locations-for-data-and-log-files.md).  
  
> [!NOTE]  
>  如果日志文件可用，[!INCLUDE[ssDE](../../includes/ssde-md.md)]将使用这些文件，而不会重新生成日志文件。  
  
 FOR ATTACH_REBUILD_LOG 具有以下要求：  
  
-   完全关闭数据库。  
  
-   所有数据文件（MDF 和 NDF）都必须可用。  
  
> [!IMPORTANT]  
>  该操作会中断日志备份链。 建议在完成该操作后执行完整数据库备份。 有关详细信息，请参阅 [BACKUP (Transact-SQL)](../../t-sql/statements/backup-transact-sql.md)。  
  
 通常，FOR ATTACH_REBUILD_LOG 用于将具有大型日志的可读/写数据库复制到另一台服务器，在这台服务器上，数据库副本频繁使用，或仅用于读操作，因而所需的日志空间少于原始数据库。  
  
 不能对数据库快照指定 FOR ATTACH_REBUILD_LOG。  
  
 有关附加和分离数据库的详细信息，请参阅[数据库分离和附加 &#40;SQL server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md).  
  
 \<filespec >  
 控制文件属性。  
  
 名称*logical_file_name*  
 指定文件的逻辑名称。 指定 FILENAME 时，需要使用 NAME，除非指定 FOR ATTACH 子句之一。 无法将 FILESTREAM 文件组命名为 PRIMARY。  
  
 *logical_file_name*  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中引用文件时所用的逻辑名称。 *Logical_file_name*必须在数据库中是唯一且符合的规则[标识符](../../relational-databases/databases/database-identifiers.md)。 名称可以是字符或 Unicode 常量，也可以是常规标识符或分隔标识符。  
  
 FILENAME { *os_file_name* | *filestream_path* **'** }  
 指定操作系统（物理）文件名称。  
  
  *os_file_name*   
 是创建文件时由操作系统使用的路径和文件名。 文件必须驻留在下列一种设备中：安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的本地服务器、存储区域网络 [SAN] 或基于 iSCSI 的网络。 执行 CREATE DATABASE 语句前，指定路径必须存在。 有关详细信息，请参阅“备注”部分的“数据库文件和文件组”。  
  
 如果为该文件指定了 UNC 路径，则可以设置 SIZE、MAXSIZE 和 FILEGROWTH 参数。  
  
 如果此文件位于原始分区， *os_file_name*必须指定现有的原始分区的驱动器号。 每个原始分区上只能创建一个数据文件。  
  
 不应将数据文件放在压缩文件系统中，除非这些文件是只读的辅助文件或数据库是只读的。 日志文件一定不要放在压缩文件系统中。  
  
  *filestream_path*   
 对于 FILESTREAM 文件组，FILENAME 指向将存储 FILESTREAM 数据的路径。 在最后一个文件夹之前的路径必须存在，但不能存在最后一个文件夹。 例如，如果指定路径 C:\MyFiles\MyFilestreamData、C:\MyFiles 必须存在才能运行 ALTER DATABASE，但 MyFilestreamData 文件夹不能存在。  
  
 必须在同一语句中创建文件组和文件 (`<filespec>`)。  
  
 SIZE 和 FILEGROWTH 属性不适用于 FILESTREAM 文件组。  
  
 大小*大小*  
 指定文件的大小。  
  
 大小不能时指定*os_file_name*指定为 UNC 路径。 SIZE 不适用于 FILESTREAM 文件组。  
  
 *大小*  
 文件的初始大小。  
  
 当*大小*对于主文件中，未提供[!INCLUDE[ssDE](../../includes/ssde-md.md)]使用模型数据库中的主文件的大小。 模型的默认大小为 8 MB (开头[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]) 或 （对于早期版本） 的 1 MB。 当指定了辅助数据文件或日志文件时，但*大小*没有为文件中，指定[!INCLUDE[ssDE](../../includes/ssde-md.md)]使文件成为 8 MB (开头[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]) 或 （对于早期版本） 的 1 MB。 为主文件指定的大小至少应与 model 数据库的主文件大小相同。  
  
 可以使用千字节 (KB)、兆字节 (MB)、千兆字节 (GB) 或兆兆字节 (TB) 后缀。 默认值为 MB。 指定一个整数，不包含小数位。 *大小*是一个整数值。 对于大于 2147483647 的值，使用更大的单位。  
  
 MAXSIZE *max_size*  
 指定文件可增大到的最大大小。 不能为 MAXSIZE 时指定*os_file_name*指定为 UNC 路径。  
  
 *max_size*  
 最大的文件大小。 可以使用 KB、MB、GB 和 TB 后缀。 默认值为 MB。 指定一个整数，不包含小数位。 如果*max_size*未指定，则该文件增长，直到磁盘已满。 *Max_size*是一个整数值。 对于大于 2147483647 的值，使用更大的单位。  
  
 UNLIMITED  
 指定文件将增长到磁盘充满。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，指定为不限制增长的日志文件的最大大小为 2 TB，而数据文件的最大大小为 16 TB。  
  
> [!NOTE]  
>  为 FILESTREAM 容器指定此选项时，没有最大大小。 它将继续增大，直到磁盘已满。  
  
 FILEGROWTH *growth_increment*  
 指定文件的自动增量。 文件的 FILEGROWTH 设置不能超过 MAXSIZE 设置。 FILEGROWTH 不能为时指定*os_file_name*指定为 UNC 路径。 FILEGROWTH 不适用于 FILESTREAM 文件组。  
  
 *growth_increment*  
 每次需要新空间时为文件添加的空间量。  
  
 该值可以 MB、KB、GB、TB 或百分比 (%) 为单位指定。 如果未在数量后面指定 MB、KB 或 %，则默认值为 MB。 如果指定 %，则增量大小为发生增长时文件大小的指定百分比。 指定的大小将舍入为最接近的 64 KB，并最小值为 64 KB。  
  
 值为 0 时表明自动增长被设置为关闭，不允许增加空间。  
  
 如果未指定 FILEGROWTH，默认值是：  
  
|版本|默认值|  
|-------------|--------------------|  
|开始[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|数据 64 MB。 日志文件 64 MB。|  
|开始[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|数据 1 MB。 10%的日志文件。|  
|之前[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|数据 10%。 10%的日志文件。|  
  
 \<文件组 >  
 控制文件组属性。 不能对数据库快照指定文件组。  
  
 文件组*filegroup_name*  
 文件组的逻辑名称。  
  
 *filegroup_name*  
 *filegroup_name*必须在数据库中唯一，并且不能为系统提供的名称主要或 PRIMARY_LOG。 名称可以是字符或 Unicode 常量，也可以是常规标识符或分隔标识符。 名称必须符合的规则[标识符](../../relational-databases/databases/database-identifiers.md)。  
  
 CONTAINS FILESTREAM  
 指定文件组在文件系统中存储 FILESTREAM 二进制大型对象 (BLOB)。  
  
 CONTAINS MEMORY_OPTIMIZED_DATA  

**适用于**:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 指定文件组在文件系统中存储内存优化数据。 有关详细信息，请参阅[内存中 OLTP&#40;内存中优化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)。 每个数据库只能有一个 MEMORY_OPTIMIZED_DATA 文件组。 创建文件组来存储内存优化数据的代码示例，请参阅[创建内存优化表和本机编译的存储过程](../../relational-databases/in-memory-oltp/creating-a-memory-optimized-table-and-a-natively-compiled-stored-procedure.md)。  
  
 DEFAULT  
 指定命名文件组为数据库中的默认文件组。  
  
 *database_snapshot_name*  
 新数据库快照的名称。 数据库快照名称必须在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例中唯一，并且必须符合标识符规则。 *database_snapshot_name*最多 128 个字符。  
  
 ON **(**名称 **=**  *logical_file_name***，** FILENAME **=** *os_file_name***)** [ **，**...*n* ]  
 若要创建数据库快照，请在源数据库中指定文件列表。 若要使快照工作，必须分别指定所有数据文件。 但是，日志文件不允许用于数据库快照。 数据库快照不支持 FILESTREAM 文件组。 如果在 CREATE DATABASE ON 子句中包含了 FILESTREAM 数据文件，该语句将失败，并且会引发错误。  
  
 有关的名称、 文件名和它们的值的说明，请参阅等效的说明\<filespec > 值。  
  
> [!NOTE]  
>  当创建数据库快照，其他\<filespec > 选项和关键字主不允许。  
  
 AS SNAPSHOT OF *source_database_name*  
 指定正在创建的数据库为指定的源数据库的数据库快照*source_database_name*。 快照和源数据库必须位于同一实例中。  
  
 有关详细信息，请参阅“备注”部分的“数据库快照”。  
  
## <a name="remarks"></a>注释  
 [Master 数据库](../../relational-databases/databases/master-database.md)应支持的任何时候创建、 修改或删除用户数据库。  
  
 CREATE DATABASE 语句必须以自动提交模式（默认事务管理模式）运行，不允许在显式或隐式事务中使用。  
  
 使用一条 CREATE DATABASE 语句即可创建数据库以及存储该数据库的文件。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 通过使用以下步骤实现 CREATE DATABASE 语句：  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用一份[模型数据库](../../relational-databases/databases/model-database.md)初始化数据库和其元数据。  
  
2.  为数据库分配 Service Broker GUID。  
  
3.  然后，[!INCLUDE[ssDE](../../includes/ssde-md.md)]使用空页填充数据库的剩余部分，包含记录数据库中空间使用情况的内部数据页除外。  
  
 在一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的实例中最多可以指定 32,767 个数据库。  
  
 每个数据库都有一个所有者，它可以在数据库中执行特殊操作。 所有者是创建数据库的用户。 可以通过更改数据库所有者[sp_changedbowner](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)。  

某些数据库功能依赖于功能或数据库的完整功能的文件系统中存在的功能。 依赖于文件系统功能集的功能的一些示例包括：
- DBCC CHECKDB
- 文件流
- 使用 VSS 和文件快照的联机备份
- 创建数据库快照
- 内存优化数据文件组
   
## <a name="database-files-and-filegroups"></a>数据库文件和文件组  
 每个数据库具有至少两个文件，*主文件*和*事务日志文件*，和至少一个文件组。 可以为每个数据库指定最多 32,767 个文件和 32,767 个文件组。  
  
 当你创建一个数据库时，使数据文件尽可能大基于最大预期在数据库中的数据量  
  
 建议使用存储区域网络 (SAN)、基于 iSCSI 的网络或本地附加的磁盘来存储 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库文件，因为该配置使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的性能和可靠性得到了优化。  
  
## <a name="database-snapshots"></a>数据库快照  
 你可以使用 CREATE DATABASE 语句创建的只读静态视图，*数据库快照*的*源数据库*。 当创建快照时，源数据库已存在，所以数据库快照在事务上与源数据库一致。 源数据库可以具有多个快照。  
  
> [!NOTE]  
>  创建数据库快照时，CREATE DATABASE 语句不能引用日志文件、脱机文件、还原文件和不存在的文件。  
  
 如果创建数据库快照失败，快照便成为可疑快照，必须将其删除。 有关详细信息，请参阅[DROP DATABASE &#40;Transact SQL &#41;](../../t-sql/statements/drop-database-transact-sql.md).  
  
 每个快照都将一直存在，直到使用 DROP DATABASE 将其删除为止。  
  
 有关详细信息，请参阅[数据库快照 (SQL Server)](../../relational-databases/databases/database-snapshots-sql-server.md)。  
  
## <a name="database-options"></a>数据库选项  
 创建数据库时，总会自动设置几个数据库选项。 有关这些选项的列表，请参阅[ALTER DATABASE SET 选项 &#40;Transact SQL &#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
## <a name="the-model-database-and-creating-new-databases"></a>model 数据库和创建新数据库  
 中的所有用户定义对象[模型数据库](../../relational-databases/databases/model-database.md)复制到所有新创建的数据库。 可以向 model 数据库中添加任何对象（例如表、视图、存储过程、数据类型等），以将这些对象包括到所有新建数据库中。  
  
 在创建数据库时*database_name*语句指定如果没有其他大小参数，则主数据文件将在模型数据库中创建主文件相同的大小。  
  
 除非指定了 FOR ATTACH，否则每个新数据库都从 model 数据库继承数据库选项设置。 例如，数据库选项自动收缩设置为**true**模型以及你创建任何新数据库中。 如果更改了 model 数据库中的选项，则这些新选项设置也将用于您所创建的所有新数据库中。 在 model 数据库中的更改操作不会影响现有数据库。 如果在 CREATE DATABASE 语句中指定了 FOR ATTACH，则新数据库将继承原始数据库的数据库选项设置。  
  
## <a name="viewing-database-information"></a>查看数据库信息  
 可以使用目录视图、系统函数和系统存储过程返回有关数据库、文件和文件组的信息。 有关详细信息，请参阅[系统变量 (Transact-SQL)](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)。  
  
## <a name="permissions"></a>Permissions  
 要求具有 CREATE DATABASE、CREATE ANY DATABASE 或 ALTER ANY DATABASE 权限。  
  
 为了控制对运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的计算机上的磁盘使用，通常只有少数登录帐户才有创建数据库的权限。  
  
 以下示例向数据库用户 Fay 提供创建数据库的权限。  
  
```  
USE master;  
GO  
GRANT CREATE DATABASE TO [Fay];  
GO  
```  
  
### <a name="permissions-on-data-and-log-files"></a>对数据文件和日志文件的权限  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，会对每个数据库的数据文件和日志文件设置特定的权限。 每当对数据库执行下列操作时，便会设置下列权限：  
  
|||  
|-|-|  
|创建时间|修改以添加新文件|  
|附加|备份|  
|分离|还原|  
  
 如果这些文件位于具有打开权限的目录中，那么以上权限可以防止文件被意外篡改。  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssExpressEd2005](../../includes/ssexpressed2005-md.md)] 不设置数据文件和日志文件权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-creating-a-database-without-specifying-files"></a>A. 创建未指定文件的数据库  
 以下示例创建名为 `mytest` 的数据库，并创建相应的主文件和事务日志文件。 因为该语句没有\<filespec > 项，主数据库文件是模型数据库主文件的大小。 事务日志将设置为下列值中的较大者：512 KB 或主数据文件大小的 25%。 因为没有指定 MAXSIZE，文件可以增大到填满所有可用的磁盘空间为止。 此示例演示如何在创建 `mytest` 数据库之前删除名为 `mytest` 的数据库（如果它存在）。  
  
```  
USE master;  
GO  
IF DB_ID (N'mytest') IS NOT NULL
DROP DATABASE mytest;
GO
CREATE DATABASE mytest;  
GO  
-- Verify the database files and sizes  
SELECT name, size, size*1.0/128 AS [Size in MBs]   
FROM sys.master_files  
WHERE name = N'mytest';  
GO  
  
```  
  
### <a name="b-creating-a-database-that-specifies-the-data-and-transaction-log-files"></a>B. 创建指定数据和事务日志文件的数据库  
 下面的示例创建数据库`Sales`。 由于未使用关键字 PRIMARY，因此第一个文件 (`Sales_dat`) 将成为主文件。 因为在 `Sales_dat` 文件的 SIZE 参数中没有指定 MB 或 KB，将使用 MB 并按 MB 分配。 创建、修改或删除用户数据库后，应备份 `Sales_log` 文件以 MB 为单位进行分配，因为 `MB` 参数中显式声明了 `SIZE` 后缀。  
  
```tsql  
USE master;  
GO  
CREATE DATABASE Sales  
ON   
( NAME = Sales_dat,  
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\saledat.mdf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 5 )  
LOG ON  
( NAME = Sales_log,  
    FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA\salelog.ldf',  
    SIZE = 5MB,  
    MAXSIZE = 25MB,  
    FILEGROWTH = 5MB ) ;  
GO  
```  
  
### <a name="c-creating-a-database-by-specifying-multiple-data-and-transaction-log-files"></a>C. 通过指定多个数据和事务日志文件创建数据库  
 以下示例创建数据库 `Archive`，该数据库具有三个 `100-MB` 数据文件和两个 `100-MB` 事务日志文件。 主文件是列表中的第一个文件，并使用 `PRIMARY` 关键字显式指定。 事务日志文件在 `LOG ON` 关键字后指定。 请注意用于 `FILENAME` 选项中各文件的扩展名：`.mdf` 用于主数据文件，`.ndf` 用于辅助数据文件，`.ldf` 用于事务日志文件。 此示例将数据库放置于 `D:` 驱动器上，而非 `master` 数据库中。  
  
```tsql  
USE master;  
GO  
CREATE DATABASE Archive   
ON  
PRIMARY    
    (NAME = Arch1,  
    FILENAME = 'D:\SalesData\archdat1.mdf',  
    SIZE = 100MB,  
    MAXSIZE = 200,  
    FILEGROWTH = 20),  
    ( NAME = Arch2,  
    FILENAME = 'D:\SalesData\archdat2.ndf',  
    SIZE = 100MB,  
    MAXSIZE = 200,  
    FILEGROWTH = 20),  
    ( NAME = Arch3,  
    FILENAME = 'D:\SalesData\archdat3.ndf',  
    SIZE = 100MB,  
    MAXSIZE = 200,  
    FILEGROWTH = 20)  
LOG ON   
   (NAME = Archlog1,  
    FILENAME = 'D:\SalesData\archlog1.ldf',  
    SIZE = 100MB,  
    MAXSIZE = 200,  
    FILEGROWTH = 20),  
   (NAME = Archlog2,  
    FILENAME = 'D:\SalesData\archlog2.ldf',  
    SIZE = 100MB,  
    MAXSIZE = 200,  
    FILEGROWTH = 20) ;  
GO  
```  
  
### <a name="d-creating-a-database-that-has-filegroups"></a>D. 创建具有文件组的数据库  
 以下示例创建数据库 `Sales`，该数据库具有以下文件组：  
  
-   文件的主文件组`Spri1_dat`和`Spri2_dat`。 将这些文件的 FILEGROWTH 增量指定为 `15%`。  
  
-   名为 `SalesGroup1` 的文件组，其中包含文件 `SGrp1Fi1` 和 `SGrp1Fi2`。  
  
-   名为 `SalesGroup2` 的文件组，其中包含文件 `SGrp2Fi1` 和 `SGrp2Fi2`。  
  
 此示例将数据和日志文件放置于不同的磁盘上，以便提高性能。  
  
```tsql  
USE master;  
GO  
CREATE DATABASE Sales  
ON PRIMARY  
( NAME = SPri1_dat,  
    FILENAME = 'D:\SalesData\SPri1dat.mdf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 15% ),  
( NAME = SPri2_dat,  
    FILENAME = 'D:\SalesData\SPri2dt.ndf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 15% ),  
FILEGROUP SalesGroup1  
( NAME = SGrp1Fi1_dat,  
    FILENAME = 'D:\SalesData\SG1Fi1dt.ndf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 5 ),  
( NAME = SGrp1Fi2_dat,  
    FILENAME = 'D:\SalesData\SG1Fi2dt.ndf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 5 ),  
FILEGROUP SalesGroup2  
( NAME = SGrp2Fi1_dat,  
    FILENAME = 'D:\SalesData\SG2Fi1dt.ndf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 5 ),  
( NAME = SGrp2Fi2_dat,  
    FILENAME = 'D:\SalesData\SG2Fi2dt.ndf',  
    SIZE = 10,  
    MAXSIZE = 50,  
    FILEGROWTH = 5 )  
LOG ON  
( NAME = Sales_log,  
    FILENAME = 'E:\SalesLog\salelog.ldf',  
    SIZE = 5MB,  
    MAXSIZE = 25MB,  
    FILEGROWTH = 5MB ) ;  
GO  
```  
  
### <a name="e-attaching-a-database"></a>E. 附加数据库  
 以下示例分离在示例 D 中创建的数据库 `Archive`，然后使用 `FOR ATTACH` 子句附加该数据库。 `Archive` 定义为具有多个数据和日志文件。 但是，由于文件的位置自创建后没有发生更改，所以只需在 `FOR ATTACH` 子句中指定主文件。 从 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 开始，要附加的数据库中包含的所有全文文件也将随数据库一起附加。  
  
```tsql  
USE master;  
GO  
sp_detach_db Archive;  
GO  
CREATE DATABASE Archive  
      ON (FILENAME = 'D:\SalesData\archdat1.mdf')   
      FOR ATTACH ;  
GO  
```  
  
### <a name="f-creating-a-database-snapshot"></a>F. 创建数据库快照  
 下面的示例创建数据库快照`sales_snapshot0600`。 由于数据库快照是只读的，所以不能指定日志文件。 为了符合语法要求，指定了源数据库中的每个文件，但没有指定文件组。  
  
 该示例的源数据库是在示例 D 中创建的 `Sales` 数据库。  
  
```tsql  
USE master;  
GO  
CREATE DATABASE sales_snapshot0600 ON  
    ( NAME = SPri1_dat, FILENAME = 'D:\SalesData\SPri1dat_0600.ss'),  
    ( NAME = SPri2_dat, FILENAME = 'D:\SalesData\SPri2dt_0600.ss'),  
    ( NAME = SGrp1Fi1_dat, FILENAME = 'D:\SalesData\SG1Fi1dt_0600.ss'),  
    ( NAME = SGrp1Fi2_dat, FILENAME = 'D:\SalesData\SG1Fi2dt_0600.ss'),  
    ( NAME = SGrp2Fi1_dat, FILENAME = 'D:\SalesData\SG2Fi1dt_0600.ss'),  
    ( NAME = SGrp2Fi2_dat, FILENAME = 'D:\SalesData\SG2Fi2dt_0600.ss')  
AS SNAPSHOT OF Sales ;  
GO  
```  
  
### <a name="g-creating-a-database-and-specifying-a-collation-name-and-options"></a>G. 创建数据库并指定排序规则名称和选项  
 下面的示例创建数据库`MyOptionsTest`。 指定了排序规则名称，并将 `TRUSTYWORTHY` 和 `DB_CHAINING` 选项设置为 `ON`。  
  
```tsql  
USE master;  
GO  
IF DB_ID (N'MyOptionsTest') IS NOT NULL  
DROP DATABASE MyOptionsTest;  
GO  
CREATE DATABASE MyOptionsTest  
COLLATE French_CI_AI  
WITH TRUSTWORTHY ON, DB_CHAINING ON;  
GO  
--Verifying collation and option settings.  
SELECT name, collation_name, is_trustworthy_on, is_db_chaining_on  
FROM sys.databases  
WHERE name = N'MyOptionsTest';  
GO  
  
```  
  
### <a name="h-attaching-a-full-text-catalog-that-has-been-moved"></a>H. 附加已移动的全文目录  
 以下示例同时附加全文目录 `AdvWksFtCat` 以及 `AdventureWorks2012` 数据和日志文件。 在该示例中，将全文目录从其默认位置移动到新位置 `c:\myFTCatalogs`。 数据和日志文件保留在其默认位置。  
  
```tsql  
USE master;  
GO  
--Detach the AdventureWorks2012 database  
sp_detach_db AdventureWorks2012;  
GO  
-- Physically move the full text catalog to the new location.  
--Attach the AdventureWorks2012 database and specify the new location of the full-text catalog.  
CREATE DATABASE AdventureWorks2012 ON   
    (FILENAME = 'c:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\AdventureWorks2012_data.mdf'),   
    (FILENAME = 'c:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\AdventureWorks2012_log.ldf'),  
    (FILENAME = 'c:\myFTCatalogs\AdvWksFtCat')  
FOR ATTACH;  
GO  
```  
  
### <a name="i-creating-a-database-that-specifies-a-row-filegroup-and-two-filestream-filegroups"></a>I. 创建指定一个行文件组和两个 FILESTREAM 文件组的数据库  
 下面的示例将创建数据库 `FileStreamDB`。 该数据库在创建之时包含一个行文件组和两个 FILESTREAM 文件组。 每个文件组都包含一个文件：  
  
-   `FileStreamDB_data` 包含行数据。 它包含一个文件，即带有默认路径的 `FileStreamDB_data.mdf`。  
  
-   `FileStreamPhotos` 包含 FILESTREAM 数据。 它包含两个 FILESTREAM 数据容器，`FSPhotos`（位于 `C:\MyFSfolder\Photos`）和 `FSPhotos2`（位于 `D:\MyFSfolder\Photos`）。 它被标记为默认 FILESTREAM 文件组。  
  
-   `FileStreamResumes` 包含 FILESTREAM 数据。 它包含一个位于位于 `FSResumes` 中的 FILESTREAM 数据容器 `C:\MyFSfolder\Resumes`。  
  
```tsql  
USE master;  
GO  
-- Get the SQL Server data path.  
DECLARE @data_path nvarchar(256);  
SET @data_path = (SELECT SUBSTRING(physical_name, 1, CHARINDEX(N'master.mdf', LOWER(physical_name)) - 1)  
                  FROM master.sys.master_files  
                  WHERE database_id = 1 AND file_id = 1);  
  
 -- Execute the CREATE DATABASE statement.   
EXECUTE ('CREATE DATABASE FileStreamDB  
ON PRIMARY   
    (  
    NAME = FileStreamDB_data   
    ,FILENAME = ''' + @data_path + 'FileStreamDB_data.mdf''  
    ,SIZE = 10MB  
    ,MAXSIZE = 50MB  
    ,FILEGROWTH = 15%  
    ),  
FILEGROUP FileStreamPhotos CONTAINS FILESTREAM DEFAULT  
    (  
    NAME = FSPhotos  
    ,FILENAME = ''C:\MyFSfolder\Photos''  
-- SIZE and FILEGROWTH should not be specified here.  
-- If they are specified an error will be raised.  
, MAXSIZE = 5000 MB  
    ),  
    (  
      NAME = FSPhotos2  
      , FILENAME = ''D:\MyFSfolder\Photos''  
      , MAXSIZE = 10000 MB  
     ),  
FILEGROUP FileStreamResumes CONTAINS FILESTREAM  
    (  
    NAME = FileStreamResumes  
    ,FILENAME = ''C:\MyFSfolder\Resumes''  
    )   
LOG ON  
    (  
    NAME = FileStream_log  
    ,FILENAME = ''' + @data_path + 'FileStreamDB_log.ldf''  
    ,SIZE = 5MB  
    ,MAXSIZE = 25MB  
    ,FILEGROWTH = 5MB  
    )'  
);  
GO  
```  
  
### <a name="j-creating-a-database-that-has-a-filestream-filegroup-with-multiple-files"></a>J. 创建一个数据库，该数据库具有含多个文件的 FILESTREAM 文件组  
 下面的示例将创建数据库 `BlobStore1`。 该数据库在创建之时包含一个行文件组和一个 FILESTREAM 文件组 `FS`。 该 FILESTREAM 文件组包含两个文件：`FS1` 和 `FS2`。 然后，通过将第三个文件 `FS3` 添加到 FILESTREAM 文件组来改变该数据库。  
  
```tsql  
USE master;  
GO  
  
CREATE DATABASE [BlobStore1]  
CONTAINMENT = NONE  
ON PRIMARY   
(   
    NAME = N'BlobStore1',   
    FILENAME = N'C:\BlobStore\BlobStore1.mdf',  
    SIZE = 100MB,  
    MAXSIZE = UNLIMITED,  
    FILEGROWTH = 1MB  
),   
FILEGROUP [FS] CONTAINS FILESTREAM DEFAULT   
(  
    NAME = N'FS1',  
    FILENAME = N'C:\BlobStore\FS1',  
    MAXSIZE = UNLIMITED  
),   
(  
    NAME = N'FS2',  
    FILENAME = N'C:\BlobStore\FS2',  
    MAXSIZE = 100MB  
)  
LOG ON   
(  
    NAME = N'BlobStore1_log',  
    FILENAME = N'C:\BlobStore\BlobStore1_log.ldf',  
    SIZE = 100MB,  
    MAXSIZE = 1GB,  
    FILEGROWTH = 1MB  
);  
GO  
  
ALTER DATABASE [BlobStore1]  
ADD FILE  
(  
    NAME = N'FS3',  
    FILENAME = N'C:\BlobStore\FS3',  
    MAXSIZE = 100MB  
)  
TO FILEGROUP [FS];  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)   
 [数据库分离和附加 (SQL Server)](../../relational-databases/databases/database-detach-and-attach-sql-server.md)   
 [DROP DATABASE (Transact SQL)](../../t-sql/statements/drop-database-transact-sql.md)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)   
 [sp_changedbowner &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-changedbowner-transact-sql.md)   
 [sp_detach_db &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)   
 [sp_removedbreplication &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md)   
 [数据库快照 (SQL Server)](../../relational-databases/databases/database-snapshots-sql-server.md)   
 [移动数据库文件](../../relational-databases/databases/move-database-files.md)   
 [数据库](../../relational-databases/databases/databases.md)   
 [二进制大型对象 (Blob) 数据 (SQL Server)](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)  

