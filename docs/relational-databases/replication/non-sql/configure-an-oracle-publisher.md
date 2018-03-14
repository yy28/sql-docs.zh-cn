---
title: "配置 Oracle 发布服务器 | Microsoft Docs"
ms.custom: 
ms.date: 09/05/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Oracle publishing [SQL Server replication], configuring
ms.assetid: 240c8416-c8e5-4346-8433-07e0f779099f
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 115247323429a5a981fdeff76ebb4d0f6d33581f
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2018
---
# <a name="configure-an-oracle-publisher"></a>配置 Oracle 发布服务器
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Oracle 发布服务器中的发布的创建方法与典型快照和事务发布相同，但在创建 Oracle 发布服务器中的发布之前，必须先完成下列步骤（本主题详细介绍步骤 1、步骤 3 和步骤 4）：  
  
1.  使用提供的脚本在 Oracle 数据库中创建复制管理用户。  
  
2.  对于发布的表，直接（而不是通过角色）将每个表的 SELECT 权限授予第一步创建的 Oracle 管理用户。  
  
3.  在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 分发服务器上安装 Oracle 客户端软件和 OLE DB 访问接口，然后重新启动 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例。 如果分发服务器运行在 64 位平台上，则必须使用 64 位版本的 Oracle OLE DB 访问接口。  
  
4.  在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 分发服务器上将 Oracle 数据库配置为发布服务器。  

[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 支持下列异类事务复制和快照复制方案：  
  
-   将数据从 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 发布到非[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器。  

-   将数据发布到 Oracle 以及从 Oracle 发布数据具有以下限制条件：  
  | |2016 或更早版本 |2017 或更高版本 |
  |-------|-------|--------|
  |从 Oracle 复制 |仅支持 Oracle 10g 或更早版本 |仅支持 Oracle 10g 或更早版本 |
  |复制到 Oracle |最高为 Oracle 12c |不支持 |

 不推荐异类复制到非 SQL Server 订阅服务器。 不推荐使用 Oracle 发布。 若要移动数据，请创建使用变更数据捕获和 [!INCLUDE[ssIS](../../../includes/ssis-md.md)]的解决方案。  


 有关 Oracle 发布服务器可以发布的对象的列表，请参阅 [Oracle 发布服务器的设计注意事项和限制](../../../relational-databases/replication/non-sql/design-considerations-and-limitations-for-oracle-publishers.md)。  
  
> [!NOTE]  
>  您必须是 **sysadmin** 固定服务器角色的成员，才能启用发布服务器或分发服务器以及创建 Oracle 发布或来自 Oracle 发布的订阅。  
  
## <a name="creating-the-replication-administrative-user-schema-within-the-oracle-database"></a>在 Oracle 数据库中创建复制管理用户架构  
 您必须创建一个用户架构，使复制代理在该用户架构的上下文中连接到 Oracle 数据库并执行操作。 必须授予此架构多种权限，下一部分列出了这些权限。 此架构拥有由 Oracle 发布服务器上的 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 复制进程创建的所有对象，但公共同义词 **MSSQLSERVERDISTRIBUTOR**除外。 有关在 Oracle 数据库中创建的对象的详细信息，请参阅 [Objects Created on the Oracle Publisher](../../../relational-databases/replication/non-sql/objects-created-on-the-oracle-publisher.md)。  
  
> [!NOTE]  
>  删除 **MSSQLSERVERDISTRIBUTOR** 公共同义词和用 **CASCADE** 选项配置的 Oracle 复制用户，会删除 Oracle 发布服务器上的所有复制对象。  
  
 有一个示例脚本可以帮助建立 Oracle 复制用户架构。 安装 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 后，该脚本位于以下目录下：*\<驱动器>*:\\\Program Files\Microsoft SQL Server\\*\<InstanceName>*\MSSQL\Install\oracleadmin.sql。 [Script to Grant Oracle Permissions](../../../relational-databases/replication/non-sql/script-to-grant-oracle-permissions.md)主题中也包括了此脚本。  
  
 使用具有 DBA 权限的帐户连接到 Oracle 数据库并执行此脚本。 此脚本将提示输入复制管理用户架构的用户名和密码以及用于创建对象的默认表空间（此表空间必须已存在于 Oracle 数据库中）。 有关为对象指定其他表空间的信息，请参阅[管理 Oracle 表空间](../../../relational-databases/replication/non-sql/manage-oracle-tablespaces.md)。 可以任选用户名和强密码，但要将它们记下来，因为以后将 Oracle 数据库配置为发布服务器时必须提供此信息。 建议只将此架构用于复制所需的对象，而不要在此架构下创建要发布的表。  
  
### <a name="creating-the-user-schema-manually"></a>手动创建用户架构  
 如果手动创建复制管理用户架构，必须通过数据库角色或直接为此架构授予下列权限。  
  
-   CREATE PUBLIC SYNONYM 和 DROP PUBLIC SYNONYM  
  
-   CREATE PROCEDURE  
  
-   CREATE SEQUENCE  
  
-   CREATE SESSION  
  
 还必须直接为用户授予下列权限（不是通过角色）：  
  
-   CREATE ANY TRIGGER。 快照和事务复制都需要此权限。  
  
-   CREATE TABLE  
  
-   CREATE VIEW  
  
## <a name="installing-and-configuring-oracle-client-networking-software-on-the-sql-server-distributor"></a>在 SQL Server 分发服务器上安装和配置 Oracle 客户端网络软件  
 必须在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 分发服务器上安装和配置 Oracle 客户端网络软件和 Oracle OLE DB 访问接口，这样分发服务器才能连接到 Oracle 发布服务器。 安装软件后，对安装软件的文件夹设置适当的权限，然后重新启动 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例以确保更新所有设置（后面的“设置目录权限”部分对权限进行了介绍）。  
  
> [!NOTE]  
>  Oracle 客户端网络软件必须是可以获得的最新版本。 Oracle 建议用户安装最新版本的客户端软件。 因此，客户端软件的版本通常比数据库软件更高。  
  
 安装和配置客户端网络软件的最直接的方法是使用 Oracle 客户端磁盘上的 Oracle Universal Installer 和 Net Configuration Assistant。  
  
 在 Oracle Universal Installer 中，必须提供以下信息：  
  
|信息|Description|  
|-----------------|-----------------|  
|Oracle 主目录|这是 Oracle 软件的安装目录的路径。 接受默认路径（C:\oracle\ora90 或类似路径），或输入另一个路径。 有关 Oracle 主目录的详细信息，请参阅本主题后面的“Oracle 主目录注意事项”部分。|  
|Oracle 主目录名称|Oracle 主目录路径的别名。|  
|安装类型|在 Oracle 10g 中，选择 **Administrator** 安装选项。|  
  
 完成 Oracle Universal Installer 之后，使用 Net Configuration Assistant 配置网络连接。 必须提供四部分信息以配置网络连接。 在设置数据库和侦听器时，Oracle 数据库管理员将配置网络。如果您没有此信息，应由数据库管理员提供此信息。 必须执行以下操作：  
  
|操作|Description|  
|------------|-----------------|  
|标识数据库|标识数据库的方法有两种。 第一种方法是使用 Oracle 系统标识符 (SID)，该方法在所有 Oracle 版本中均可用。 第二种方法是使用服务名称，该名称从 Oracle 8.0 版本开始才可用。 这两种方法都使用一个在创建数据库时所配置的值，并且要注意，客户端网络配置所使用的命名方法要与管理员在配置数据库的侦听器时使用的命名方法相同。|  
|标识数据库的网络别名|必须指定网络别名，该别名将用来访问 Oracle 数据库。 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 分发服务器上将 Oracle 数据库标识为发布服务器时，也要提供此别名。 实际上，网络别名是指向在创建数据库时所配置的远程 SID 或服务名称的指针。在不同的 Oracle 版本和产品中存在多种引用名称，包括 Net 服务名称和 TNS 别名。 在登录时，SQL*Plus 将提示您输入此别名来作为“Host String”参数。|  
|选择网络协议|选择要支持的相应协议。 大多数应用程序使用 TCP。|  
|指定主机信息以标识数据库侦听器|主机是正在运行 Oracle 侦听器的计算机的名称或 DNS 别名，该计算机通常是该数据库所驻留的计算机。 对于某些协议，必须提供其他信息。 例如，如果选择 TCP，则必须提供相应的端口，以便侦听器侦听针对目标数据库的连接请求。 默认 TCP 配置使用 1521 端口。|  
  
### <a name="setting-directory-permissions"></a>设置目录权限  
 在分发服务器上运行 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服务时所使用的帐户，必须对 Oracle 客户端网络软件的安装目录（和所有子目录）具有读取和执行权限。  
  
### <a name="testing-connectivity-between-the-sql-server-distributor-and-the-oracle-publisher"></a>测试 SQL Server 分发服务器和 Oracle 发布服务器之间的连接  
 Net Configuration Assistant 快要结束的时候，可能会出现一个测试 Oracle 发布服务器连接的选项。 在测试连接之前，请确保 Oracle 数据库实例已联机，并且 Oracle 侦听器正在运行。 如果测试不成功，请与负责所要连接的数据库的 Oracle DBA 联系。  
  
 成功连接到 Oracle 发布服务器后，请尝试使用与您所创建的复制管理用户架构关联的帐户和密码登录数据库。 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服务所使用的 Windows 帐户下运行时必须执行下列操作：  
  
1.  单击 **“启动”**，再单击 **“运行”**。  
  
2.  键入 `cmd` ，然后单击 **“确定”**。  
  
3.  在命令提示符下，键入：  
  
     `sqlplus <UserSchemaLogin>/<UserSchemaPassword>@<NetServiceName>`  
  
     例如： `sqlplus replication/$tr0ngPasswerd@Oracle90Server`  
  
4.  如果网络配置成功，将成功登录，并显示 `SQL` 提示符。  
  
5.  如果在连接到 Oracle 数据库时出现问题，请参阅 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的“ [ssNoVersion](../../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md)。  
  
### <a name="considerations-for-oracle-home"></a>Oracle 主目录注意事项  
 Oracle 支持并行安装应用程序二进制文件，但是，在给定时间复制过程只能使用一组二进制文件。 每组二进制文件都与一个 Oracle 主目录关联。二进制文件位于 %ORACLE_HOME%\bin 目录中。 复制过程中与 Oracle 发布服务器建立连接时，必须确保使用正确的二进制文件集（尤其是客户端网络软件的最新版本）。  
  
 使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服务和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 代理服务所使用的帐户登录到分发服务器，并设置相应的环境变量。 应将 %ORACLE_HOME% 变量设置为引用在安装客户端网络软件时所指定的安装点。 %PATH% 必须包括 %ORACLE_HOME% \bin 目录作为所遇到的第一个 Oracle 项。 有关设置环境变量的信息，请参阅 Windows 文档。  
  
## <a name="configuring-the-oracle-database-as-a-publisher-at-the-sql-server-distributor"></a>在 SQL Server 分发服务器上将 Oracle 数据库配置为发布服务器  
 Oracle 发布服务器总是使用远程分发服务器。您必须配置一个 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例以作为 Oracle 发布服务器的分发服务器（一个 Oracle 发布服务器只能使用一个分发服务器，但单个分发服务器可以为多个 Oracle 发布服务器提供服务）。 配置分发服务器后，通过 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 、Transact-SQL 或复制管理对象 (RMO)，在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]分发服务器上将 Oracle 数据库实例标识为发布服务器。 有关如何配置分发服务器的详细信息，请参阅[配置分发](../../../relational-databases/replication/configure-distribution.md)。  
  
> [!NOTE]  
>  Oracle 发布服务器不能与它的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 分发服务器同名，也不能与任何使用同一分发服务器的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 发布服务器同名。  
  
 将 Oracle 数据库标识为发布服务器时，必须选择 Oracle 发布选项：“完整”或“Oracle 网关”。 标识发布服务器后，除非删除并重新配置发布服务器，否则无法更改此选项。 “完整”选项用于为快照和事务发布提供 Oracle 发布的完整的支持功能集。 Oracle Gateway 选项提供特定的设计优化，以提高当复制作为系统间的网关时的性能。  
  
 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 分发服务器上标识 Oracle 发布服务器后，复制创建一个链接服务器，其名称与 Oracle 数据库的 TNS 服务名相同。 此链接服务器只能由复制使用。 如果需要通过链接服务器连接来连接到 Oracle 发布服务器，请创建另一个 TNS 服务名称，然后在调用 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) 时使用该名称。  
  
 若要配置 Oracle 发布服务器和创建发布，请参阅 [Create a Publication from an Oracle Database](../../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Oracle 发布服务器的管理注意事项](../../../relational-databases/replication/non-sql/administrative-considerations-for-oracle-publishers.md)   
 [Oracle 发布服务器的数据类型映射](../../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)   
 [有关 Oracle 发布的术语词汇表](../../../relational-databases/replication/non-sql/glossary-of-terms-for-oracle-publishing.md)   
 [Oracle 发布概述](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  
