---
title: 创建链接服务器
ms.date: 01/24/2020
ms.prod: sql
ms.technology: ''
ms.prod_service: database-engine
ms.reviewer: carlrab
ms.topic: conceptual
f1_keywords:
- sql13.swb.linkedserver.properties.general.f1
- sql13.swb.linkedserver.properties.security.f1
- sql13.swb.linkedserver.properties.provider.f1
- sql13.swb.linkedserver.properties.options.f1
helpviewer_keywords:
- linked servers [SQL Server], creating
ms.assetid: 3228065d-de8f-4ece-a9b1-e06d3dca9310
author: stevestein
ms.author: sstein
ms.custom: seo-dt-2019
ms.openlocfilehash: ddcead69006fdee32598590192e777984ea3fcd7
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "76761888"
---
# <a name="create-linked-servers-sql-server-database-engine"></a>创建链接服务器（SQL Server 数据库引擎）
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  本主题说明如何通过使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 创建链接服务器和访问来自其他 [!INCLUDE[tsql](../../includes/tsql-md.md)]的数据。 通过创建链接服务器，您可以使用来自多个数据源的数据。 该链接服务器不必是其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例，尽管这种情况很常见。  
  
##  <a name="background"></a><a name="Background"></a> 背景  
 链接服务器让用户可以对 OLE DB 数据源进行分布式异类查询。 在创建某一链接服务器后，可对该服务器运行分布式查询，并且查询可以联接来自多个数据源的表。 如果链接服务器定义为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例，则可执行远程存储过程。  
  
 链接服务器的功能和必需的参数可能会有很大差异。 本主题中的示例是典型示例，但并未描述所有选项。 有关详细信息，请参阅 [sp_addlinkedserver (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)的数据。  
  
##  <a name="security"></a><a name="Security"></a> Security  
  
### <a name="permissions"></a>权限  
 在使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句时，需要具有 **ALTER ANY LINKED SERVER** 权限，或需要具有 **setupadmin** 固定服务器角色中的成员资格。 使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 时，要求具有 **CONTROL SERVER** 权限，或者具有 **sysadmin** 固定服务器角色的成员身份。  
  
##  <a name="how-to-create-a-linked-server"></a><a name="Procedures"></a> 如何创建链接服务器  
 您可以使用以下任意一项：  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
##### <a name="to-create-a-linked-server-to-another-instance-of-sql-server-using-sql-server-management-studio"></a>使用 SQL Server Management Studio 创建与其他 SQL Server 实例的链接服务器  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，打开对象资源管理器，展开 **“服务器对象”** ，右键单击 **“链接服务器”** ，然后单击 **“新建链接服务器”** 。  
  
2.  在 **“常规”** 页上的 **“链接服务器”** 框中，键入您链接到的 **SQL Server** 实例的名称。  
  
     **SQL Server**  
     将链接服务器标识为 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的实例。 如果您使用此方法来定义某个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 链接服务器，则在 **“链接服务器”** 中指定的名称必须是该服务器的网络名称。 另外，从该服务器上检索的所有表都来自该链接服务器上为相应登录名所定义的默认数据库。  
  
     **其他数据源**  
     指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以外的 OLE DB 服务器类型。 单击此选项将激活其下面的选项。  
  
     **提供程序**  
     从列表框中选择 OLE DB 数据源。 OLE DB 访问接口是使用注册表中给定的 PROGID 注册的。  
  
     **产品名称**  
     键入要作为链接服务器添加的 OLE DB 数据源的产品名称。  
  
     **数据源**  
     根据 OLE DB 访问接口的说明，键入数据源名称。 如果要连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的实例，请提供实例名称。  
  
     **访问接口字符串**  
     键入与数据源相对应的 OLE DB 访问接口的唯一编程标识符 (PROGID)。 有关有效访问接口字符串的示例，请参阅 [sp_addlinkedserver (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)的数据。  
  
     **位置**  
     根据 OLE DB 访问接口的说明，键入数据库的位置。  
  
     **目录**  
     键入在连接 OLE DB 访问接口时要使用的目录的名称。  
  
     若要测试能否连接到链接服务器，请在对象资源管理器中，右键单击链接服务器，然后单击 **“测试连接”** 。  
  
    > [!NOTE]  
    >  如果该 **SQL Server** 实例是默认实例，则输入承载 **SQL Server**实例的计算机的名称。 如果该 **SQL Server** 是命名实例，则输入计算机名称和实例名称，例如 **Accounting\SQLExpress**。  
  
3.  在“服务器类型”区域中，选择 SQL Server 以便指示该链接服务器是 SQL Server的另一个实例    。  
  
4.  在 **“安全性”** 页上，指定在原始 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 连接到链接服务器时将使用的安全上下文。 在通过使用其域登录名连接用户的域环境中，选择“使用登录名的当前安全上下文建立连接”通常是最佳选择  。 在用户通过使用 **SQL Server** 登录名连接到原始 **SQL Server** 时，最佳选择通常是选择 **“通过使用此安全上下文”** ，然后提供在链接服务器上进行身份验证时所必需的凭据。  
  
     **本地登录**  
     指定可连接到链接服务器的本地登录。 本地登录可以是使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证的登录，也可以是使用 Windows 身份验证的登录。 使用此列表可以将连接限定为特定的登录，也可以允许某些登录使用其他登录名进行连接。  
  
     **Impersonate**  
     将用户名和密码从本地登录传递到链接服务器。 对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证，具有完全相同的名称和密码的登录必须存在于远程服务器中。 对于 Windows 登录，登录必须是链接服务器中的有效登录。  
  
     若要使用模拟功能，配置必须满足委托的要求。  
  
     **远程用户**  
     使用远程用户映射 **“本地登录”** 中未定义的用户。 **“远程用户”** 必须是远程服务器中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证登录。  

    > [!WARNING]
    > 在 Azure SQL 数据库托管实例部署中，只能将 SQL Server 用户用作“远程用户”。  

     **远程密码**  
     指定远程用户的密码。  
  
     **添加**  
     添加新的本地登录。  
  
     **删除**  
     删除现有的本地登录。  
  
     **不建立连接**  
     指定不对列表中未定义的登录建立连接。  
  
     **不使用安全上下文建立连接**  
     指定对于列表中未定义的登录，不使用安全上下文建立连接。  
  
     **使用登录当前的安全上下文建立连接**  
     指定对于列表中未定义的登录，使用登录的当前安全上下文建立连接。 如果使用 Windows 身份验证连接到本地服务器，则使用 Windows 凭据连接到远程服务器。 如果使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证连接到本地服务器，则在连接到远程服务器时需要使用登录名和密码。 在这种情况下，具有完全相同的名称和密码的登录必须存在于远程服务器中。  
  
     **使用此安全上下文建立连接**  
     指定对于列表中未定义的登录，使用 **“远程登录”** 和 **“使用密码”** 框中指定的登录名和密码建立连接。 远程登录必须是远程服务器中的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证登录。  
  
5.  或者，若要查看或指定服务器选项，请单击 **“服务器选项”**  页。  
  
     **排序规则兼容**  
     影响分布式查询在链接服务器上的执行。 如果该选项设置为 true，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 假定链接服务器中的所有字符在字符集和排序规则（或排序顺序）上与本地服务器兼容。 这使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 得以将字符列上的比较发送给提供程序。 如果没有设置该选项，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将始终在本地进行字符列上的比较。  
  
     只有在确信链接服务器所对应的数据源与本地服务器有相同的字符集和排序顺序时，才应当设置该选项。  
  
     **数据访问**  
     启用和禁用链接服务器以进行分布式查询访问。  
  
     **RPC**  
     从指定的服务器启用 RPC。  
  
     **RPC Out**  
     对指定的服务器启用 RPC。  
  
     **使用远程排序规则**  
     确定是使用远程列的排序规则还是使用本地服务器的排序规则。  
  
     如果为 True，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据源将使用远程列的排序规则，并且非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据源将使用排序规则名称指定的排序规则。  
  
     如果为 False，则分布式查询将始终使用本地服务器的默认排序规则，而排序规则名称和远程列的排序规则将被忽略。 默认值为 false。  
  
     **排序规则名称**  
     如果“使用远程排序规则”为 True，并且数据源不是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据源，则指定远程数据源使用的排序规则名称。 此名称必须是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]支持的排序规则之一。  
  
     如果访问的是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以外的 OLE DB 数据源，但该数据源的排序规则与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的某个排序规则匹配，则使用该选项。  
  
     链接服务器必须支持该服务器中所有列使用的单个排序规则。 如果链接服务器支持单个数据源内的多个排序规则，或者如果无法确定链接服务器的排序规则是否与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的某个排序规则匹配，则不要设置该选项。  
  
     **连接超时值**  
     连接到链接服务器时的超时值（秒）。  
  
     如果为 0，则使用 **sp_configure** 默认 [远程登录超时](../../database-engine/configure-windows/configure-the-remote-login-timeout-server-configuration-option.md) 选项值。  
  
     **查询超时值**  
     链接服务器上执行的查询的超时值（秒）。  
  
     如果为 0，则使用 **sp_configure** 默认 [远程查询超时](../../database-engine/configure-windows/configure-the-remote-query-timeout-server-configuration-option.md) 选项值。  
  
     **启用分布式事务处理的升级**  
     使用该选项可通过 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 分布式事务处理协调器 (MS DTC) 事务保护服务器到服务器的操作过程。 如果该选项是 TRUE，则调用远程存储过程将启动分布式事务，并用 MS DTC 登记该事务。 有关详细信息，请参阅 [sp_serveroption (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)的数据。  
  
6.  单击“确定”。   
  
##### <a name="to-view-the-provider-options"></a>查看提供程序选项  
  
-   若要查看提供程序提供的选项，请单击 **“提供程序选项”** 页。  
  
     每个访问接口的选项都各不相同。 例如，某些类型的数据提供索引，有些则没有提供。 使用此对话框可以帮助 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 理解访问接口的功能。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装某些常用的数据访问接口，但在提供数据的产品发生更改时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装的访问接口可能不支持所有最新的功能。 提供数据的产品功能的有关信息的最佳来源是针对该产品的文档。  
  
     **动态参数**  
     表明访问接口允许对参数化查询使用“?”参数标记语法。 仅当该访问接口支持 **ICommandWithParameters** 接口并支持“?”作为参数标记时，才应设置此选项。 如果设置了此选项，则允许 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 针对该访问接口执行参数化查询。 这种对访问接口执行参数化查询的能力会提高某些查询的性能。  
  
     **嵌套查询**  
     指示访问接口允许在 FROM 子句中使用嵌套的 `SELECT` 语句。 如果设置了此选项，则允许 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将某些查询委托给需要在 FROM 子句中嵌套 SELECT 语句的访问接口。  
  
     **仅零级**  
     只对访问接口调用 0 级的 OLE DB 接口。  
  
     **允许进程内**  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 允许将访问接口实例化为进程内服务器。 如果未设置此选项，则默认行为是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程外实例化访问接口。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程外实例化访问接口，可防止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程在访问接口中出错。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程外实例化访问接口时，不允许更新或插入长的引用列（**text**、 **ntext**或 **image**）。  
  
     **非事务更新**  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 允许更新，即使 **ITransactionLocal** 不可用时也是如此。 如果启用此选项，对访问接口的更新将不可恢复，因为该访问接口不支持事务。  
  
     **作为访问路径的索引**  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 尝试使用访问接口的索引来提取数据。 默认情况下，索引只能用于元数据而且从不打开。  
  
     **禁止即席访问**  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不允许通过 OPENROWSET 和 OPENDATASOURCE 函数对 OLE DB 访问接口进行即席访问。 如果未设置此选项，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 同样不允许进行即席访问。  
  
     **支持 "Like" 运算符**  
     指示访问接口支持使用 LIKE 关键字的查询。  
  
###  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
 若要通过使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 创建链接服务器，请使用 [sp_addlinkedserver (Transact SQL)](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)[CREATE LOGIN (Transact SQL)](../../t-sql/statements/create-login-transact-sql.md) 和 [sp_addlinkedsrvlogin (Transact SQL)](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md) 语句。  
  
##### <a name="to-create-a-linked-server-to-another-instance-of-sql-server-using-transact-sql"></a>使用 Transact-SQL 创建与其他 SQL Server 实例的链接服务器  
  
1.  在查询编辑器中，输入以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 命令以便链接到名为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 `SRVR002\ACCTG`实例：  
  
    ```sql  
    USE [master]  
    GO  
    EXEC master.dbo.sp_addlinkedserver   
        @server = N'SRVR002\ACCTG',   
        @srvproduct=N'SQL Server' ;  
    GO  
  
    ```  
  
2.  执行以下代码，以便将链接服务器配置为使用正在使用链接服务器的登录名的域凭据。  
  
    ```sql  
    EXEC master.dbo.sp_addlinkedsrvlogin   
        @rmtsrvname = N'SRVR002\ACCTG',   
        @locallogin = NULL ,   
        @useself = N'True' ;  
    GO  
  
    ```  
  
##  <a name="follow-up-steps-to-take-after-you-create-a-linked-server"></a><a name="FollowUp"></a> 跟进：在创建链接服务器后采取的步骤  
  
#### <a name="to-test-the-linked-server"></a>测试链接服务器  
  
-   执行下面的代码，测试与链接服务器的连接。 以下示例返回链接服务器上数据库的名称。  
  
    ```sql  
    SELECT name FROM [SRVR002\ACCTG].master.sys.databases ;  
    GO  
  
    ```  
  
#### <a name="writing-a-query-that-joins-tables-from-a-linked-server"></a>编写联接来自某一链接服务器的多个表的查询  
  
-   使用由四部分组成的名称引用链接服务器上的对象。 执行以下代码，以便返回本地服务器上所有登录名的列表及其在链接服务器上的匹配登录名。  
  
    ```sql  
    SELECT local.name AS LocalLogins, linked.name AS LinkedLogins  
    FROM master.sys.server_principals AS local  
    LEFT JOIN [SRVR002\ACCTG].master.sys.server_principals AS linked  
        ON local.name = linked.name ;  
    GO  
    ```  
  
     如果为链接服务器登录名返回了 NULL，则意味着该登录名在链接服务器上不存在。 这些登录名将无法使用链接服务器，除非链接服务器配置为传递不同的安全上下文或者链接服务器接受匿名连接。  
  
## <a name="see-also"></a>另请参阅  
 [链接服务器（数据库引擎）](../../relational-databases/linked-servers/linked-servers-database-engine.md)   
 [sp_addlinkedserver (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_serveroption (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)  
  
  
