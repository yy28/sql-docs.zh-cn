---
title: 使用复制数据库向导 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.cdw.transfermethod.f1
- sql12.swb.cdw.welcome.f1
- sql12.swb.cdw.packageconfiguration.f1
- sql12.swb.cdw.schedule.f1
- sql12.swb.cdw.destination.f1
- sql12.swb.cdw.complete.f1
- sql12.swb.cdw.destinationconfiguration.f1
- sql12.swb.cdw.selectdatabaseobjects.f1
- sql12.swb.cdw.databases.f1
- sql12.swb.cdw.source.f1
- sql12.swb.cdw.locationofsourcedbfiles.f1
helpviewer_keywords:
- Copy Database Wizard
- starting Copy Database Wizard
ms.assetid: 7a999fc7-0a26-4a0d-9eeb-db6fc794f3cb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e72b960db0fd5b733119cafeca98f124eaa15f38
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62871134"
---
# <a name="use-the-copy-database-wizard"></a>使用复制数据库向导
  通过复制数据库向导，可以方便地将数据库及其对象从一台服务器移动或复制到另一台服务器，而服务器无需停机。 还可以将数据库从以前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。 使用此向导可执行以下操作：  
  
-   选取源服务器和目标服务器。  
  
-   选择要移动、复制或升级的数据库。  
  
-   为数据库指定文件位置。  
  
-   在目标服务器上创建登录名。  
  
-   复制其他支持的对象、作业、用户定义的存储过程和错误消息。  
  
-   计划何时移动或复制数据库。  
  
 除了复制数据库，还可以复制关联的元数据，例如 **master** 数据库的登录名和对象，它们是复制的数据库所必需的。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [先决条件](#Prerequisites)  
  
     [建议](#Recommendations)  
  
     [安全性](#Security)  
  
-   **使用复制数据库向导：**  
  
     [复制、 移动或升级数据库](#Copy_Move)  
  
-   **升级后，请按照，操作：**  
  
     [升级 SQL Server 数据库之后](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   在 Express 版本中未提供复制数据库向导。  
  
-   复制数据库向导不能用于复制或移动以下数据库。  
  
    -   系统数据库  
  
    -   为复制操作标记的数据库。  
  
    -   标记为“无法访问”、“正在加载”、“脱机”、“正在恢复”、“可疑”或处于“紧急模式”的数据库。  
  
-   升级数据库后，它无法降级到以前的版本。  
  
-   如果选择 **“移动”** 选项，则在移动数据库之后，该向导将自动删除源数据库。 如果选择 **“复制”** 选项，则复制数据库向导不会删除源数据库。  
  
-   如果使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理对象方法移动全文目录，则必须在移动后重新填充索引。  
  
-   分离和附加方法可分离数据库，移动或复制数据库 .mdf、.ndf、.ldf 文件，并在新的位置重新附加该数据库。 对于分离和附加方法，若要避免数据丢失或不一致，不能将活动会话附加到正在移动或复制的数据库。 如果存在活动会话，复制数据库向导不会执行移动或复制操作。 对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理对象方法，由于数据库从不会脱机，因此允许活动会话。  
  
###  <a name="Prerequisites"></a> 先决条件  
 确保在目标服务器上启动了 SQL Server 代理。  
  
###  <a name="Recommendations"></a> 建议  
  
-   为了确保升级后的数据库具有最佳性能，请对升级后的数据库运行 sp_updatestats（更新统计信息）。  
  
-   将数据库复制到另一个服务器实例时，为了给用户和应用程序提供一致的体验，您最好在另一个服务器实例上重新创建该数据库的部分或全部元数据（例如登录名和作业）。 有关详细信息，请参阅 [当数据库在其他服务器实例上可用时管理元数据 (SQL Server)](manage-metadata-when-making-a-database-available-on-another-server.md)。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
 您必须是源服务器和目标服务器上 **sysadmin** 固定服务器角色的成员。  
  
##  <a name="Copy_Move"></a> 复制、 移动或升级数据库  
  
1.  在中[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，在对象资源管理器中，展开**数据库**，右键单击某个数据库，指向**任务**，然后单击**复制数据库**。  
  
2.  从 **“选择源服务器”** 页，指定要移动或复制的数据库所在的服务器并输入登录信息。 在选择身份验证方法并输入登录信息之后，单击 **“下一步”** 即可与源服务器建立连接。 此连接会在整个会话过程中保持打开状态。  
  
     **源服务器**  
     选择你想要移动或复制的数据库所在的服务器的名称或单击浏览 (**...**) 按钮以找到所需的服务器。 该服务器必须至少为 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]。  
  
     **Use Windows Authentication**  
     允许用户通过 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 用户帐户进行连接。  
  
     **Use SQL Server Authentication**  
     允许用户通过提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证用户名和密码进行连接。  
  
     **用户名**  
     输入连接所使用的用户名。 只有选择使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证进行连接时，此选项才可用。  
  
     **密码**  
     输入登录名的密码。 只有选择使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证进行连接时，此选项才可用。  
  
     **Next**  
     连接到服务器并验证用户。 此过程将检查用户是否是所选计算机上 **sysadmin** 固定服务器角色的成员。  
  
3.  从 **“选择目标服务器”** 页，指定数据库移动或复制的目标服务器。 如果将源服务器和目标服务器设置为同一个服务器实例，则将会创建一个数据库的副本。 在此情况下，必须稍后在向导中重命名数据库。 仅当目标服务器上不存在名称冲突时，源数据库名称才能用于复制或移动的数据库。 如果存在名称冲突，则必须在目标服务器上手动解决冲突问题，然后才能在此处使用源数据库名称。  
  
     **目标服务器**  
     选择向其或多个数据库将被移动或复制，或单击浏览的服务器的名称 (**...**) 按钮以找到目标服务器。  
  
    > [!NOTE]  
    >  可以使用群集服务器作为目标；复制数据库向导将确保您只选择群集目标服务器上的共享驱动器。  
  
     **Use Windows Authentication**  
     允许用户通过 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 用户帐户进行连接。  
  
     **Use SQL Server Authentication**  
     允许用户通过提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证用户名和密码进行连接。  
  
     **用户名**  
     输入连接所使用的用户名。 只有选择 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证时，此选项才可用。  
  
     **密码**  
     输入登录名的密码。 只有选择 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证时，此选项才可用。  
  
     **Next**  
     连接到服务器并验证用户。 此过程检查用户是否对所选计算机拥有上述权限。  
  
4.  从 **“选择传输方法”** 页，选择传输方法。  
  
     **使用分离和附加方法**  
     从源服务器上分离数据库，将数据库文件（.mdf、.ndf 和 .ldf）复制到目标服务器，然后在目标服务器上附加数据库。 此方法通常较快，因为其主要任务只是读取源磁盘和写入目标磁盘。 无需使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 逻辑在数据库中创建对象或创建数据存储结构。 但是，如果数据库包含大量已分配但未使用的空间，此方法会比较慢。 例如，对于一个在创建时分配了 100 MB 空间的几乎为空的新数据库，即使只使用了 5 MB 空间，也会复制全部 100 MB 空间。  
  
    > [!NOTE]  
    >  如果使用此方法。用户将无法在传输过程中使用数据库。  
  
     **如果失败，则重新附加源数据库**  
     数据库复制之后，原始数据库文件将始终重新附加到源服务器。 如果无法完成数据库移动，请使用此框将原始文件重新附加到源数据库。  
  
     **使用 SQL 管理对象方法**  
     此方法读取源数据库上每个数据库对象的定义，在目标数据库上创建每个对象。 然后，它从源表向目标表传输数据，重新创建索引和元数据。  
  
    > [!NOTE]  
    >  数据库用户可以在传输过程中继续访问数据库。  
  
5.  从 **“选择数据库”** 页，选择要从源服务器移动或复制到目标服务器的数据库。 请参阅本主题“开始之前”一节中的 [限制和局限](#Restrictions) 。  
  
     **“移动”**  
     将数据库移动到目标服务器。  
  
     **“复制”**  
     将数据库复制到目标服务器。  
  
     **数据源**  
     显示源服务器上的数据库。  
  
     **“状态”**  
     显示**确定**如果可以移动该数据库。 否则将显示无法移动该数据库的原因。  
  
     **刷新**  
     刷新数据库列表。  
  
     **Next**  
     开始验证过程，然后转到下一屏幕。  
  
6.  从“配置目标数据库”  页，更改数据库名称（如果适用）并指定数据库文件的位置和名称。 在移动或复制每个数据库时都会出现此页。  
  
7.  从 **“选择数据库对象”** 页，选择要在移动或复制操作中包括的对象。 只有当源和目标为不同服务器的时候，此页才可用。 若要包含某个对象，请在“可用相关对象”框中单击对象名称，然后单击 **>>** 按钮，将该对象移动到“所选相关对象”框中。 若要排除某个对象，请在“所选相关对象”框中单击对象名称，然后单击 **<\<** 按钮，将该对象移动到“可用相关对象”框中。 默认情况下，将传输每个所选类型中的所有对象。 若要选择某个类型中的单个对象，请在 **“所选相关对象”** 框中单击该对象类型旁边的省略号按钮。 这将打开一个对话框，您可以从中选择各个对象。  
  
     **登录名 （在运行时所有登录名）**  
     在移动或复制操作中包括登录名。 默认为选中状态。  
  
     **master 数据库中的存储过程**  
     包含从存储的过程**主**移动或复制操作中的数据库。  
  
    > [!NOTE]  
    >  不能对扩展存储过程及其相关的 DLL 进行自动复制。  
  
     **SQL Server 代理作业**  
     包括从作业**msdb**移动或复制操作中的数据库。  
  
     **用户定义的错误消息**  
     在移动或复制操作中包括用户定义的错误消息。  
  
     **端点**  
     包括源数据库中定义的端点。  
  
     **全文目录**  
     包括源数据库中的全文目录。  
  
     **SSIS 包**  
     包括源数据库中定义的 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 包。  
  
     **说明**  
     对象的说明。  
  
8.  从 **“源数据库文件的位置”** 页，指定源服务器上包含数据库文件的文件系统共享。 如果源服务器实例和目标服务器实例位于不同的计算机上，这是必需的。  
  
     **“数据库”**  
     显示正在移动的每个数据库的名称。  
  
     **文件夹位置**  
     指定文件系统上源数据库文件所在的位置。  
  
     例如：C:\Program Files\Microsoft SQL Server\MSSQL110.MSSQLSERVER\MSSQL\DATA  
  
     **源服务器上的文件共享**  
     指定源数据库文件的位置作为文件共享的路径。  
  
     例如:"\\\\*server_name*\C$\Program Files\Microsoft SQL Server\MSSQL110。MSSQLSERVER\MSSQL\Data  
  
9. 复制数据库向导将创建一个要传输数据库的 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 包。从 **“配置包”** 页，对包进行自定义（如果适用）。  
  
     **包位置**  
     显示 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 包的写入位置。  
  
     **包名称**  
     输入 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 包的名称。  
  
     **日志记录选项**  
     选择是将日志记录信息存储在 Windows 事件日志中还是文本文件中。  
  
     **错误日志文件路径**  
     提供日志文件位置的路径。 只有在选择了文本文件日志记录选项后，才能使用此选项。  
  
10. 从 **“安排运行包”** 页，指定希望何时启动移动操作或复制操作。 如果您不是系统管理员，必须指定有权访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SSIS) 包执行子系统的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 代理的代理帐户。  
  
     **Run immediately**  
     启动移动或复制操作，在单击后**下一步**。  
  
     **“计划”**  
     以后启动移动操作或复制操作。 当前的计划设置显示在说明框中。 若要更改该计划，请单击 **“更改”**。  
  
     **更改**  
     打开**新建作业计划**对话框。  
  
     **Integration Services 代理帐户**  
     选择可用的代理帐户。 若要计划传输，则必须至少有一个代理帐户可供用户使用，而且必须将该帐户配置为拥有对 **“SQL Server Integration Services 包执行”** 子系统的权限。  
  
     若要创建的代理帐户[!INCLUDE[ssIS](../../includes/ssis-md.md)]包执行，在对象资源管理器中的，展开**SQL Server 代理**，展开**代理**，右键单击**SSIS 包执行**，然后依次**新的代理**。  
  
     **sysadmin** 固定服务器角色的成员可以选择 **“SQL Server 代理服务帐户”**，该帐户拥有必要的权限。  
  
11. 从 **“完成该向导”** 页，查看所选选项的摘要。 单击 **“上一步”** 可以更改选项。 单击 **“完成”** 将创建数据库。 在传输过程中， **“正在执行操作”** 页会监视与 **“复制数据库向导”** 的执行有关的状态信息。  
  
     **操作**  
     列出要执行的每项操作。  
  
     **“状态”**  
     指示操作总体来说是成功还是失败。  
  
     **Message**  
     提供每个步骤返回的任何消息。  
  
##  <a name="FollowUp"></a> 跟进：在升级 SQL Server 数据库之后  
 使用复制数据库向导将数据库从早期版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 升级到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]后，该数据库将立即变为可用，然后自动升级。 如果数据库具有全文检索，升级过程将导入、重置或重新生成它们，具体取决于 **全文升级选项** 服务器属性的设置。 如果将升级选项设置为“导入”或“重新生成”，在升级过程中将无法使用全文检索。 导入可能需要数小时，而重新生成所需的时间最多时可能十倍于此，具体取决于要编制索引的数据量。 另请注意，当升级选项设置为“导入”时，如果全文目录不可用，将重新生成关联的全文检索。 有关查看或更改“全文升级选项”属性设置的信息，请参阅[管理和监视服务器实例的全文搜索](../search/manage-and-monitor-full-text-search-for-a-server-instance.md)。  
  
 如果升级前用户数据库的兼容级别为 100 或更高，升级后将保持相应级别。 如果兼容级别为 90，则在升级后的数据库中，兼容级别将设置为 100，该级别为 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 支持的最低兼容级别。 有关详细信息，请参阅 [ALTER DATABASE 兼容级别 (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)。  
  
## <a name="see-also"></a>请参阅  
 [使用分离和附加来升级数据库 (Transact-SQL)](upgrade-a-database-using-detach-and-attach-transact-sql.md)   
 [创建 SQL Server 代理的代理帐户](../../ssms/agent/create-a-sql-server-agent-proxy.md)  
  
  
