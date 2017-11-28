---
title: "ALTER DATABASE 数据库镜像 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/17/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- witness [SQL Server], establishing
- manual failover [SQL Server]
- ALTER DATABASE statement, database mirroring
- database mirroring [SQL Server], Transact-SQL
ms.assetid: 27a032ef-1cf6-4959-8e67-03d28c4b3465
caps.latest.revision: "22"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: b08f208ce80eb1e8c79d2e47a06fdd9f1de8a986
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="alter-database-transact-sql-database-mirroring"></a>ALTER DATABASE (Transact SQL) 数据库镜像 
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 改为使用 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]。  
  
 控制数据库的数据库镜像。 使用数据库镜像选项指定的值适用于数据库的副本以及整个数据库镜像会话。 只有一个\<database_mirroring_option > 允许每个 ALTER DATABASE 语句。  
  
> [!NOTE]  
>  我们建议你配置数据库镜像在非高峰时间，因为配置会影响性能。  
  
 有关 ALTER DATABASE 选项，请参阅[ALTER DATABASE &#40;Transact SQL &#41;](../../t-sql/statements/alter-database-transact-sql.md). 有关 ALTER DATABASE SET 选项，请参阅[ALTER DATABASE SET 选项 &#40;Transact SQL &#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
ALTER DATABASE database_name   
SET { <partner_option> | <witness_option> }  
  <partner_option> ::=  
    PARTNER { = 'partner_server'   
            | FAILOVER   
            | FORCE_SERVICE_ALLOW_DATA_LOSS  
            | OFF  
            | RESUME   
            | SAFETY { FULL | OFF }  
            | SUSPEND   
            | TIMEOUT integer  
            }  
  <witness_option> ::=  
    WITNESS { = 'witness_server'   
            | OFF   
            }  
  
```  
  
## <a name="arguments"></a>参数  
  
> [!IMPORTANT]  
>  SET PARTNER 或 SET WITNESS 命令在输入时可以成功完成，但随后失败。  
  
> [!NOTE]  
>  ALTER DATABASE 数据库镜像选项对于包含数据库不可用。  
  
 *database_name*  
 要修改的数据库的名称。  
  
 合作伙伴\<partner_option >  
 控制用于定义数据库镜像会话的故障转移伙伴及其行为的数据库属性。 有些 SET PARTNER 选项可对任一伙伴进行设置；而其他选项则仅限于对主体服务器或镜像服务器进行设置。 有关详细信息，请参阅下文所述的各个 PARTNER 选项。 无论在哪个伙伴上指定 SET PARTNER 子句，该子句都会影响数据库的两个副本。  
  
 若要执行 SET PARTNER 语句，必须将两个合作伙伴的端点的 STATE 都设置为 STARTED。 另请注意，必须将每个伙伴服务器实例的数据库镜像端点的 ROLE 设置为 PARTNER 或 ALL。 有关如何指定终结点的信息，请参阅[创建数据库镜像终结点为 Windows 身份验证 &#40;Transact SQL &#41;](../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md). 若要了解服务器实例的数据库镜像端点的角色和状态，请使用以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句：  
  
```  
SELECT role_desc, state_desc FROM sys.database_mirroring_endpoints  
```  
  
 **\<partner_option >:: =**  
  
> [!NOTE]  
>  只有一个\<partner_option > 允许每个 SET PARTNER 子句。  
  
  *partner_server*   
 指定在新数据库镜像会话中用作故障转移伙伴的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的服务器网络地址。 每个会话需要两个伙伴：一个作为主体服务器启动，另一个作为镜像服务器启动。 建议这两个伙伴驻留在不同的计算机上。  
  
 在每个伙伴上，为每个会话指定一次此选项。 启动数据库镜像会话需要两个 ALTER DATABASE*数据库*SET PARTNER **=***partner_server*语句. 这两个语句的顺序非常重要。 首先，连接到镜像服务器，并指定主体服务器实例作为*partner_server* (SET PARTNER **=***principal_server*). 其次，连接到主体服务器，并指定镜像服务器实例作为*partner_server* (SET PARTNER **=***mirror_server*);这将启动数据库镜像这些两个合作伙伴之间的会话。 有关详细信息，请参阅本主题后面的 [设置数据库镜像 (SQL Server)](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md)。  
  
 值*partner_server*是服务器网络地址。 其语法如下所示：  
  
 TCP**://***\<system-address>***:***\<port>*  
  
 其中  
  
-   *\<系统地址 >*是一个字符串，例如系统名称、 完全限定的域名或 IP 地址，明确标识目标计算机系统。  
  
-   *\<端口 >*是与伙伴服务器实例的镜像端点的端口号。  
  
 有关详细信息，请参阅 [指定服务器网络地址（数据库镜像）](../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md)。  
  
 下面的示例演示 SET PARTNER **=***partner_server*子句：  
  
```  
'TCP://MYSERVER.mydomain.Adventure-Works.com:7777'  
```  
  
> [!IMPORTANT]  
>  如果会话是使用 ALTER DATABASE 语句而不是 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 设置的，则默认情况下该会话将设置为完全事务安全（SAFETY 设置为 FULL），并在无自动故障转移功能的高安全模式下运行。 若要允许自动故障转移，请配置见证服务器；若要在高性能模式下运行，请关闭事务安全性 (SAFETY OFF)。  
  
 FAILOVER  
 手动将故障从主体服务器转移到镜像服务器。 只能在主体服务器上指定 FAILOVER。 此选项仅在 SAFETY 设置为 FULL（默认设置）时有效。  
  
 故障转移选项要求**master**作为数据库上下文。  
  
 FORCE_SERVICE_ALLOW_DATA_LOSS  
 未发生自动故障转移时，在数据库处于不同步状态或处于同步状态的情况下当主体服务器失败后，强制数据库服务转向镜像数据库。  
  
 强烈建议仅在主体服务器不再运行时强制运行该服务。 否则，某些客户端可能会继续访问原始主体数据库而不是新的主体数据库。  
  
 FORCE_SERVICE_ALLOW_DATA_LOSS 仅在镜像服务器上可用，且下列条件必须全部成立：  
  
-   主体服务器已关闭。  
  
-   WITNESS 设置为 OFF，或者将见证服务器连接到镜像服务器。  
  
 仅当您愿意为立即还原数据库服务而承担部分数据丢失的风险时，才能强制服务运行。  
  
 强制服务会挂起会话，并暂时将所有数据保留在原始的主体数据库中。 一旦原始主体服务器进入服务状态并且能够与新的主体服务器通信时，数据库管理员就可以恢复服务。 如果会话恢复，则所有未发送的日志记录和对应的更新都会丢失。  
  
 OFF  
 删除数据库镜像会话，并从数据库中删除镜像。 可以在任一伙伴上指定 OFF。 有关信息，请参阅有关删除镜像的影响，请参阅[删除数据库镜像 &#40;SQL server&#41;](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md).  
  
 RESUME  
 恢复挂起的数据库镜像会话。 只能在主体服务器上指定 RESUME。  
  
 SAFETY { FULL | OFF }  
 设置事务安全的级别。 只能在主体服务器上指定 SAFETY。  
  
 默认值为 FULL。 与完整的安全，数据库镜像会话同步运行 (在*高安全性模式*)。 如果安全设置为 OFF，数据库镜像会话以异步方式运行 (在*高性能模式*)。  
  
 高安全模式的行为部分取决于见证服务器，如下所示：  
  
-   当安全性设置为 FULL 并且已为该会话设置了见证服务器时，会话将在高安全模式下运行，并且具有自动故障转移功能。 失去主体服务器时，如果数据库被同步并且镜像服务器实例和见证服务器仍然相互连接（即它们有仲裁），则会话将自动进行故障转移。 有关详细信息，请参阅[仲裁：见证服务器如何影响数据库可用性（数据库镜像）](../../database-engine/database-mirroring/quorum-how-a-witness-affects-database-availability-database-mirroring.md)。  
  
     如果为会话设置了见证服务器，但是当前已断开见证服务器的连接，则镜像服务器的丢失会导致主体服务器出现故障。  
  
-   当安全性设置为 FULL 并且已将见证服务器设置为 OFF 时，会话将在高安全模式下运行，但没有自动故障转移功能。 如果镜像服务器实例出现故障，则不会影响主体服务器实例。 如果主体服务器实例出现故障，则可以将服务（可能丢失数据）强制转到镜像服务器实例。  
  
 如果将 SAFETY 设置为 OFF，则会话将在高性能模式下运行，并且不支持自动故障转移和手动故障转移。 但是，镜像服务器的问题不会影响主体服务器，如果主体服务器实例出现故障，必要时可以将服务（可能丢失数据）强制转到镜像服务器实例（如果 WITNESS 设置为 OFF，或者见证服务器当前与镜像服务器连接）。 有关强制服务的详细信息，请参阅这一部分前面的 "FORCE_SERVICE_ALLOW_DATA_LOSS"。  
  
> [!IMPORTANT]  
>  高性能模式并非旨在使用见证服务器。 但是，我们强烈建议您只要将 SAFETY 设置为 OFF，就应确保也将 WITNESS 设置为 OFF。  
  
 SUSPEND  
 暂停数据库镜像会话。  
  
 可以在任一伙伴上指定 SUSPEND。  
  
 超时*整数*  
 以秒为单位指定超时期限。 超时期限是指镜像会话中一个服务器实例在考虑断开另一实例的连接之前，等待接收来自该实例的 PING 消息的最长时间。  
  
 只能在主体服务器上指定 TIMEOUT 选项。 如果不指定此选项，则在默认情况下，超时期限为 10 秒。 如果指定 5 或更高，则超时期限将设置为指定的秒数。 如果将超时值指定为 0 到 4 秒之间，则超时期限将自动设置为 5 秒。  
  
> [!IMPORTANT]  
>  我们建议您将超时期限保持为 10 秒或更长。 如果将值设置为低于 10 秒，则可能使高负荷系统丢失 PING 并声明错误故障。  
  
 有关详细信息，请参阅 [Possible Failures During Database Mirroring](../../database-engine/database-mirroring/possible-failures-during-database-mirroring.md)。  
  
 见证服务器\<witness_option >  
 控制定义数据库镜像见证服务器的数据库属性。 SET WITNESS 子句会影响数据库的两个副本，但只能在主体服务器上指定 SET WITNESS。 服务的数据库，而不考虑的安全性设置; 如果为会话设置了见证服务器，需仲裁有关详细信息，请参阅[仲裁： 如何见证服务器会影响数据库可用性 （; 数据库镜像) #41;](../../database-engine/database-mirroring/quorum-how-a-witness-affects-database-availability-database-mirroring.md)。  
  
 建议使见证服务器和故障转移伙伴驻留在单独服务器上。 有关见证服务器的信息，请参阅[数据库镜像见证服务器](../../database-engine/database-mirroring/database-mirroring-witness.md)。  
  
 若要执行 SET WITNESS 语句，必须将主体服务器和见证服务器实例端点的 STATE 都设置为 STARTED。 另请注意，必须将见证服务器实例的数据库镜像端点的 ROLE 设置为 WITNESS 或 ALL。 有关指定终结点的信息，请参阅[数据库镜像终结点 &#40;SQL server&#41;](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md).  
  
 若要了解服务器实例的数据库镜像端点的角色和状态，请使用以下 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句：  
  
```  
SELECT role_desc, state_desc FROM sys.database_mirroring_endpoints  
```  
  
> [!NOTE]  
>  不能在见证服务器上设置数据库属性。  
  
 **\<witness_option >:: =**  
  
> [!NOTE]  
>  只有一个\<witness_option > 允许每个 SET WITNESS 子句。  
  
  *witness_server*   
 指定一个[!INCLUDE[ssDE](../../includes/ssde-md.md)]实例，作为数据库镜像会话的见证服务器。 只能在主体服务器上指定 SET WITNESS 语句。  
  
 在设置见证服务器**=***witness_server*语句的语法*witness_server*的语法相同*partner_server*。  
  
 OFF  
 从数据库镜像会话中删除见证服务器。 将见证服务器设置为 OFF 会禁用自动故障转移。 如果数据库设置为 FULL SAFETY 并且见证服务器设置为 OFF，则镜像服务器上的故障会导致主体服务器使该数据库不可用。  
  
## <a name="remarks"></a>注释  
  
## <a name="examples"></a>示例  
  
### <a name="a-creating-a-database-mirroring-session-with-a-witness"></a>A. 创建具有见证服务器的数据库镜像会话  
 设置具有见证服务器的数据库镜像会话需要配置安全性并准备镜像数据库，还需要使用 ALTER DATABASE 设置伙伴。 完成安装过程的示例，请参阅[设置数据库镜像 &#40;SQL server&#41;](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md).  
  
### <a name="b-manually-failing-over-a-database-mirroring-session"></a>B. 对数据库镜像会话进行手动故障转移  
 可从任一数据库镜像伙伴启动手动故障转移。 进行故障转移之前，应验证您认为是当前主体服务器的服务器是否确实是主体服务器。 例如，对于 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库，请在您认为是当前主体服务器的服务器实例上执行以下查询：  
  
```  
SELECT db.name, m.mirroring_role_desc   
FROM sys.database_mirroring m   
JOIN sys.databases db  
ON db.database_id = m.database_id  
WHERE db.name = N'AdventureWorks2012';   
GO  
```  
  
 如果该服务器实例确实是主体，则 `mirroring_role_desc` 的值为 `Principal`。 如果此服务器实例是镜像服务器，则 `SELECT` 语句将返回 `Mirror`。  
  
 下面的示例假定该服务器是当前主体。  
  
1.  将故障手动转移到数据库镜像伙伴：  
  
    ```  
    ALTER DATABASE AdventureWorks2012 SET PARTNER FAILOVER;  
    GO  
    ```  
  
2.  若要验证新镜像上的故障转移的结果，请执行以下查询：  
  
    ```  
    SELECT db.name, m.mirroring_role_desc   
    FROM sys.database_mirroring m   
    JOIN sys.databases db  
    ON db.database_id = m.database_id  
    WHERE db.name = N'AdventureWorks2012';   
    GO  
    ```  
  
     现在，`mirroring_role_desc` 的当前值为 `Mirror`。  
  
## <a name="see-also"></a>另请参阅  
 [CREATE DATABASE (SQL Server Transact-SQL)](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [DATABASEPROPERTYEX (Transact-SQL)](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [sys.database_mirroring_witnesses &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)  
  
  
