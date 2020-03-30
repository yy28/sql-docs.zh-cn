---
title: 数据库属性（“镜像”页）| Microsoft Docs
ms.custom: ''
ms.date: 08/25/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.databaseproperties.mirroring.f1
ms.assetid: 5bdcd20f-532d-4ee6-b2c7-18dbb7584a87
author: stevestein
ms.author: sstein
ms.openlocfilehash: a25b2b40b147cd0bd23e8c7554e548b6a577d539
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "68099594"
---
# <a name="database-properties-mirroring-page"></a>数据库属性（“镜像”页）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  从主体数据库中访问此页，并用它来配置并修改数据库的数据库镜像的属性。 还可以使用该页来启动配置数据库镜像安全向导，以查看镜像会话的状态，并可以暂停或删除数据库镜像会话。  
  
> **重要说明！！！** 开始镜像前必须先配置安全性。 如果镜像尚未开始，则必须使用此向导来开始。 **“镜像”** 页文本框将被禁用，直到向导完成为止。  
  
 **使用 SQL Server Management Studio 配置数据库镜像**  
  
-   [使用 Windows 身份验证建立数据库镜像会话 (SQL Server Management Studio)](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
## <a name="options"></a>选项  
 **配置安全性**  
 单击此按钮可以启动 **配置数据库镜像安全向导。**  
  
 如果向导成功完成，所采取的操作将取决于镜像是否已经开始，具体情况如下：  
  
|||  
|-|-|  
|如果镜像尚未开始。|属性页将缓存连接信息，并且缓存一个指示镜像数据库是否具有伙伴属性集的值。<br /><br /> 在该向导结尾，将提示您使用默认服务器网络地址和运行模式开始数据库镜像。 如果需要更改地址或运行模式，请单击 **“不开始镜像”** 。|  
|如果镜像已经开始。|如果在向导中更改了见证服务器，它将相应地进行设置。|  
  
 **服务器网络地址**  
 每种服务器实例都有一个等效选项：“主体”  、“镜像”  和“见证服务器”  。  
  
 服务器实例的服务器网络地址是在完成配置数据库镜像安全向导时自动指定的。 完成该向导后，可以根据需要手动修改网络地址。  
  
 服务器网络地址的基本语法如下：  
  
 TCP **://** _fully_qualified_domain_name_ **:** _port_  
  
 其中  
  
-   *fully_qualified_domain_name* 是服务器实例所在的服务器。  
  
-   *port* 是指分配给服务器实例的数据库镜像端点的端口。  
  
     服务器必须具有数据库镜像端点，才可参与数据库镜像。 使用配置数据库镜像安全向导建立某个服务器实例的第一个镜像会话时，该向导会自动创建端点，并将其配置为使用 Windows 身份验证。 有关如何利用基于证书的身份验证来使用此向导的信息，请参阅 [使用 Windows 身份验证建立数据库镜像会话 (SQL Server Management Studio)](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)。  
  
    >**重要说明!!**  不管要支持多少镜像会话，每个服务器实例都必须有且仅有一个数据库镜像端点。  
  
 例如，对于名为 `DBSERVER9` 的计算机系统上的服务器实例，如果其端点使用端口 `7022`，则网络地址可能为：  
  
```  
TCP://DBSERVER9.COMPANYINFO.ADVENTURE-WORKS.COM:7022  
```  
  
 有关详细信息，请参阅 [指定服务器网络地址（数据库镜像）](../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md)。  
  
> **注意：** 在数据库镜像会话期间，不能更改主体服务器和镜像服务器实例；但是可以在会话期间更改见证服务器实例。 有关详细信息，请参阅本主题后面的“备注”。  
  
 **开始镜像**  
 当满足以下所有条件时，单击此项可开始镜像：  
  
-   必须存在镜像数据库。  
  
     必须在通过使用 WITH NORECOVERY 将最近的完整备份（可能还会包括主体数据库的日志备份）还原到镜像服务器，创建了镜像数据库之后，才可以开始镜像。 有关详细信息，请参阅 [为镜像准备镜像数据库 (SQL Server)](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)的各版本中均未提供见证服务器实例。  
  
-   主体服务器实例和镜像服务器实例的 TCP 地址已经在 **服务器网络地址** 部分中指定。  
  
-   如果运行模式设置为“带自动故障转移功能的高安全(同步)”，那么还会指定镜像服务器实例的 TCP 地址。  
  
-   安全性已经正确配置。  
  
 单击 **“开始镜像”** 即可开始会话。 数据库引擎将尝试自动连接到镜像伙伴，以验证镜像服务器是否正确地进行了配置，然后开始镜像会话。 如果可以开始镜像，将创建一个作业以监控数据库。  
  
 **暂停** 或 **恢复**  
 在数据库镜像会话期间，单击“暂停”  以暂停会话。 此时，将显示一个提示，要求您确认；如果单击 **“是”** ，则会话将暂停，并且该按钮改为 **“恢复”** 。 若要恢复会话，请单击 **“恢复”** 。  
  
 有关暂停会话的影响的信息，请参阅 [暂停和恢复数据库镜像 (SQL Server)](../../database-engine/database-mirroring/pausing-and-resuming-database-mirroring-sql-server.md)。  
  
> **重要说明!!** 在强制服务后，当原始的主体服务器重新连接时，镜像将挂起。 在这种情况下，恢复镜像可能会导致原始主体服务器上的数据丢失。 有关如何管理潜在数据丢失的信息，请参阅 [数据库镜像会话期间的角色切换 (SQL Server)](../../database-engine/database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md)。  
  
 **取消镜像**  
 在主体服务器实例中，单击以停止会话，并从数据库中取消镜像配置。 此时，将显示一个提示，要求您确认；如果单击 **“是”** ，则会话将停止，并且取消镜像。 有关取消数据库镜像有何影响的信息，请参阅 [删除数据库镜像 (SQL Server)](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md)。  
  
> **注意：** 如果这是服务器实例中唯一的镜像数据库，则会取消该监视作业。  
  
 **故障转移**  
 单击此项可在发生故障时手动地将相关操作从主体数据库转移到镜像数据库。  
  
> **注意：** 如果镜像会话在高性能模式下运行，则不支持手动故障转移。 若要手动进行故障转移，必须先将运行模式更改为“不带自动故障转移功能的高安全(同步)”  。 在故障转移完成后，可将新主体服务器实例上的模式再改为“高性能(异步)”  。  
  
 此时，将显示一个提示，要求您进行确认。 如果单击 **“是”** ，将尝试进行故障转移。 主体服务器将开始尝试使用 Windows 身份验证连接到镜像服务器。 如果 Windows 身份验证无效，主体服务器将显示 **“连接到服务器”** 对话框。 如果镜像服务器使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证，请选择 **“身份验证”** 框中的 **“SQL Server 身份验证”** 。 在 **“登录名”** 文本框中，指定连接镜像服务器时使用的登录帐户，然后在 **“密码”** 文本框中指定该帐户的密码。  
  
 如果故障转移成功， **“数据库属性”** 对话框关闭。 主体服务器和镜像服务器角色互换：以前的镜像数据库成为主体数据库，而主体数据库成为镜像数据库。 请注意， **“数据库属性”** 对话框在以前的主体数据库中随即不可用，因为该数据库已变为镜像数据库；而在故障转移后，此对话框在新的主体数据库中将会可用。  
  
 如果故障转移失败，将显示一条错误消息，并且该对话框保持打开状态。  
  
> **重要说明!!** 如果在 **“数据库属性”** 对话框中修改了属性后单击 **“故障转移”** ，这些更改将会丢失。 若要保存当前的更改，请在确认提示中回答 **“否”** ，再单击 **“确定”** 保存更改。 然后，重新打开“数据库属性”对话框，再单击 **“故障转移”** 。  
  
 **运行模式**  
 根据需要，可以选择更改运行模式。 某些运行模式的可用性取决于是否为见证服务器指定了 TCP 地址。 选项如下：  
  
|选项|是否需要见证服务器？|说明|  
|------------|--------------|-----------------|  
|**高性能(异步)**|空(如果存在，尚未使用但会话需要仲裁)|为获得最佳性能，镜像数据库始终在某种程度上滞后于主体数据库，永远无法完全同步。 但是，数据库之间的异步间隔通常很小。 丢失伙伴会产生以下影响：<br /><br /> 如果镜像服务器实例变为不可用，则主体服务器继续可用。<br /><br /> 如果主体服务器实例变为不可用，则镜像停止。 但如果该会话没有见证服务器（推荐）或见证服务器已连接到镜像服务器，则镜像服务器将保持可作为热备用服务器访问；数据库所有者可以强制该服务镜像服务器实例（可能会造成数据丢失）。|  
|**不带自动故障转移功能的高安全(同步)**|否|保证将所有提交的事务都写入镜像服务器的磁盘上。<br /><br /> 如果伙伴彼此连接在一起，便可进行手动故障转移。<br /><br /> 丢失伙伴会产生以下影响：<br /><br /> 如果镜像服务器实例变为不可用，则主体服务器继续可用。<br /><br /> 如果主体服务器实例变为不可用，则镜像服务器实例会停止但仍可以作为热备用；数据库所有者可以强制让镜像服务器实例来提供服务（但这样做可能会丢失数据）。|  
|**带自动故障转移功能的高安全(同步)**|是（必需）|通过包含见证服务器实例以支持自动故障转移，来实现最高可用性。 注意，只有首先指定了见证服务器地址，才可以选择 **“带自动故障转移功能的高安全(同步)”** 选项。<br /><br /> 只要伙伴彼此连接在一起，便可进行手动故障转移。<br /><br /> **&#42;&#42; 重要提示 &#42;&#42;** 如果见证服务器断开连接，则伙伴必须彼此连接，数据库才可用。 有关详细信息，请参阅[仲裁：见证服务器如何影响数据库可用性（数据库镜像）](../../database-engine/database-mirroring/quorum-how-a-witness-affects-database-availability-database-mirroring.md)。<br /><br /> 在同步运行模式中，所有提交的事务都保证会受到保护，写入到镜像服务器的磁盘上。 如果存在见证服务器，丢失伙伴连接会有以下影响：<br /><br /> 如果主体服务器实例变为不可用，则会发生自动故障转移。 镜像服务器实例将充当主体服务器，并且将其数据库用作主体数据库。<br /><br /> 如果镜像服务器实例变为不可用，则主体服务器继续可用。<br /><br /> <br /><br /> 有关详细信息，请参阅 [Database Mirroring Operating Modes](../../database-engine/database-mirroring/database-mirroring-operating-modes.md)。|  
  
 在镜像开始后，您可以更改运行模式，并可以通过单击 **“确定”** 来保存更改。  
  
 有关运行模式的详细信息，请参阅 [Database Mirroring Operating Modes](../../database-engine/database-mirroring/database-mirroring-operating-modes.md)。  
  
 **Status**  
 镜像开始以后，“状态”  面板将显示从你选择“镜像”  页时起数据库镜像会话的状态。 若要更新 **“状态”** 面板，请单击 **“刷新”** 按钮。 可能的状态如下：  
  
|States|说明|  
|------------|-----------------|  
|**尚未配置此数据库用于镜像**|不存在数据库镜像会话，并且没有要在 **“镜像”** 页上报告的活动。|  
|**已暂停**|主体数据库可用，但没有向镜像服务器发送任何日志。|  
|**无连接**|主体服务器实例无法与其伙伴建立连接。|  
|**正在同步**|镜像数据库的内容滞后于主体数据库的内容。 主体服务器实例正在向镜像服务器实例发送日志记录，这会对镜像数据库应用更改，使其前滚。<br /><br /> 在数据库镜像会话开始时，镜像数据库和主体数据库处于此状态。|  
|**故障转移**|在主体服务器实例中，手动故障转移（角色切换）已开始，服务器当前正转换为镜像角色。 在此状态中，到主体数据库的用户连接将快速终止，并且数据库将立即接管镜像角色。|  
|**已同步**|当镜像服务器与主体服务器几乎保持同步时，数据库状态将改为 **“已同步”** 。 只要主体服务器继续向镜像服务器发送更改，并且镜像服务器继续将更改应用于镜像数据库，数据库就会保持此状态。<br /><br /> 对于高安全模式，可以进行故障转移，并且没有任何数据丢失。<br /><br /> 对于高性能模式，可能总会有些数据丢失，即使在 **已同步** 状态中也是如此。|  
  
 有关详细信息，请参阅[镜像状态 (SQL Server)](../../database-engine/database-mirroring/mirroring-states-sql-server.md)。  
  
 **“刷新”**  
 单击此项可更新“状态”  框。  
  
## <a name="remarks"></a>备注  
 如果你不熟悉数据库镜像，请参阅 [数据库镜像 (SQL Server)](../../database-engine/database-mirroring/database-mirroring-sql-server.md)。  
  
### <a name="adding-a-witness-to-an-existing-session"></a>向现有会话中添加见证服务器  
 可以向现有会话中添加见证服务器，也可以替换现有的见证服务器。 如果您知道见证服务器的服务器网络地址，则可在 **“见证服务器”** 字段中手动输入该地址。 如果您不知道见证服务器的服务器网络地址，则可使用配置数据库镜像安全向导来配置见证服务器。 当该字段中出现该地址后，请确保已选中“带自动故障转移功能的高安全(同步)”  选项。  
  
 配置了新的见证服务器后，必须单击 **“确定”** 将其添加到镜像会话中。  
  
 **使用 Windows 身份验证时添加见证服务器**  
  
 [添加或替换数据库镜像见证服务器 (SQL Server Management Studio)](../../database-engine/database-mirroring/add-or-replace-a-database-mirroring-witness-sql-server-management-studio.md)  
  
### <a name="removing-a-witness"></a>删除见证服务器  
 若要删除见证服务器，请从 **“见证服务器”** 字段中删除它的服务器网络地址。 如果从具有自动故障转移功能的高安全性模式切换到高性能模式，则将自动清除“见证服务器”  字段。  
  
 删除了见证服务器后，必须单击 **“确定”** ，才能从镜像会话中将其删除。  
  
### <a name="monitoring-database-mirroring"></a>监视数据库镜像  
 若要监视服务器实例中的镜像数据库，可以使用数据库镜像监视器或 sp_dbmmonitorresults 系统存储过程。  
  
 **监视镜像数据库**  
  
-   [启动数据库镜像监视器 (SQL Server Management Studio)](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)  
  
-   [sp_dbmmonitorresults (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md)  
  
 有关详细信息，请参阅 [监视数据库镜像 (SQL Server)](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)。  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 相关任务  
  
-   [指定服务器网络地址（数据库镜像）](../../database-engine/database-mirroring/specify-a-server-network-address-database-mirroring.md)  
  
-   [使用 Windows 身份验证建立数据库镜像会话 (SQL Server Management Studio)](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
-   [启动数据库镜像监视器 (SQL Server Management Studio)](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)  
  
## <a name="see-also"></a>另请参阅  
 [针对数据库镜像和 AlwaysOn 可用性组的传输安全性 (SQL Server)](../../database-engine/database-mirroring/transport-security-database-mirroring-always-on-availability.md)   
 [数据库镜像会话期间的角色切换 (SQL Server)](../../database-engine/database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md)   
 [监视数据库镜像 (SQL Server)](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [数据库镜像 (SQL Server)](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [暂停和恢复数据库镜像 (SQL Server)](../../database-engine/database-mirroring/pausing-and-resuming-database-mirroring-sql-server.md)   
 [删除数据库镜像 (SQL Server)](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md)   
 [数据库镜像见证服务器](../../database-engine/database-mirroring/database-mirroring-witness.md)  
  
  
