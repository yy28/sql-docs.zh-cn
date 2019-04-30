---
title: 还原数据库备份 (SQL Server Management Studio) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.locatebackupfileazure.f1
- sql12.swb.specifybackup.f1
helpviewer_keywords:
- full backups [SQL Server]
- database restores [SQL Server], full backups
- backing up databases [SQL Server], full backups
- database backups [SQL Server], full backups
- restoring databases [SQL Server], full backups
ms.assetid: 24b3311d-5ce0-4581-9a05-5c7c726c7b21
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3d20276a90a64ca414b8bb6253b03df08908a1f1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62921240"
---
# <a name="restore-a-database-backup-sql-server-management-studio"></a>还原数据库备份 (SQL Server Management Studio)
  本主题说明如何还原完整数据库备份。  
  
> [!IMPORTANT]  
>  在完整恢复模式或大容量日志恢复模式下，必须先备份活动事务日志（称为日志尾部），然后才能在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中还原数据库。 有关详细信息，请参阅 [备份事务日志 (SQL Server)](back-up-a-transaction-log-sql-server.md)数据库还原到一个新位置并且可以选择重命名该数据库。 若要还原已加密的数据库，您必须有权访问用于对数据库进行加密的证书或非对称密钥。 如果没有证书或非对称密钥，数据库将无法还原。 因此，只要需要该备份，就必须保留用于对数据库加密密钥进行加密的证书。 有关详细信息，请参阅 [SQL Server Certificates and Asymmetric Keys](../security/sql-server-certificates-and-asymmetric-keys.md)。  
  
 请注意，如果您将 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 或更高版本的数据库还原为 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]，将自动升级该数据库。 通常，该数据库将立即可用。 但是，如果 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 数据库具有全文检索，则升级过程将导入、重置或重新生成它们，具体取决于“全文升级选项”服务器属性的设置。 如果将升级选项设置为“导入”或“重新生成”，在升级过程中将无法使用全文检索。 导入可能需要数小时，而重新生成所需的时间最多时可能十倍于此，具体取决于要编制索引的数据量。 另请注意，当升级选项设置为“导入”时，如果全文目录不可用，将重新生成关联的全文检索。 有关查看或更改“全文升级选项”属性设置的信息，请参阅[管理和监视服务器实例的全文搜索](../search/manage-and-monitor-full-text-search-for-a-server-instance.md)。  
  
### <a name="to-restore-a-full-database-backup"></a>还原完整数据库备份  
  
1.  连接到相应的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]实例之后，在对象资源管理器中，单击服务器名称以展开服务器树。  
  
2.  展开 **“数据库”**。 根据具体的数据库，选择一个用户数据库，或展开“系统数据库”并选择一个系统数据库。  
  
3.  右键单击该数据库，指向**任务**，依次指向**还原**，然后单击**数据库**，这将打开**Restore Database**对话框。  
  
4.  在 **“常规”** 页上，使用 **“源”** 部分指定要还原的备份集的源和位置。 选择以下选项之一：  
  
    -   **“数据库”**  
  
         从下拉列表中选择要还原的数据库。 此列表仅包含已根据 **msdb** 备份历史记录进行备份的数据库。  
  
    > [!NOTE]  
    >  如果备份是从另一台服务器执行的，则目标服务器不具有指定数据库的备份历史记录信息。 这种情况下，请选择 **“设备”** 以手动指定要还原的文件或设备。  
  
    -   **“设备”**  
  
         单击“浏览”按钮 (**...**) 以打开“选择备份设备”对话框。 在 **“备份介质类型”** 框中，从列出的设备类型中选择一种。 若要为 **“备份介质”** 框选择一个或多个设备，请单击 **“添加”**。  
  
         将所需设备添加到 **“备份介质”** 列表框后，单击 **“确定”** 返回到 **“常规”** 页。  
  
         在“源:设备:数据库”列表框中，选择应还原的数据库名称**。  
  
        > [!NOTE]  
        >  此列表仅在选择了 **“设备”** 时才可用。 只有在所选设备上具有备份的数据库才可用。  
  
         **备份介质**  
         选择还原操作的介质：**文件**，**磁带**， **URL**或**备份设备**。 只有在计算机上装有磁带机时，才会显示 **“磁带”** 选项，只有至少存在一个备份设备时，才会显示 **“备份设备”** 选项。  
  
         **备份位置**  
         查看、添加或删除还原操作使用的介质。 列表最多可以包含 64 个文件、磁带或备份设备。  
  
         **“添加”**  
         将添加到备份设备的位置**备份位置**列表。 根据您在 **“备份介质”** 字段中选择的介质类型，单击 **“添加”** 将打开下列对话框之一。  
  
        |介质类型|对话框|Description|  
        |----------------|----------------|-----------------|  
        |**File**|**定位备份文件**|在此对话框中，您可以从树中选择一个本地文件，或使用完全限定的通用命名约定 (UNC) 名称指定一个远程文件。 有关详细信息，请参阅 [备份设备 (SQL Server)](backup-devices-sql-server.md)。|  
        |**设备**|**选择备份设备**|在此对话框中，您可以从服务器实例中定义的逻辑备份设备列表中进行选择。|  
        |**磁带**|**选择备份磁带**|在此对话框中，您可以从与运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的计算机物理连接的磁带机列表中进行选择。|  
        |**URL**|这会按以下顺序启动两个对话框：<br /><br /> 1)**连接到 Windows Azure 存储**<br /><br /> 2)**在 Windows Azure 中查找备份文件**|在 **“连接到 Windows Azure 存储”**  对话框中，选择存储有 Windows Azure 存储帐户名称和访问密钥信息的现有 SQL 凭据，或通过指定存储帐户名称和存储访问密钥信息创建新的 SQL 凭据。 有关详细信息，请参阅[连接到 Windows Azure 存储&#40;还原&#41;](connect-to-microsoft-azure-storage-restore.md)。<br /><br /> 在 **“查找备份文件”** 对话框中，您可以从左边框架显示的容器列表中选择一个文件。|  
  
         如果列表已满，此 **“添加”** 按钮将不可用。  
  
         **删除**  
         删除一个或多个选定的文件、磁带或逻辑备份设备。  
  
         **目录**  
         显示选定文件、磁带或逻辑备份设备的介质内容。  
  
5.  在 **“目标”** 部分中， **“数据库”** 框自动填充要还原的数据库的名称。 若要更改数据库名称，请在 **“数据库”** 框中输入新名称。  
  
6.  在 **“还原到”** 框中，保留默认选项 **“至最近一次进行的备份”** ，或者单击 **“时间线”** 访问 **“备份时间线”** 对话框以手动选择要停止恢复操作的时间点。 有关指定特定时间点的详细信息，请参阅 [Backup Timeline](backup-timeline.md)。  
  
7.  在 **“要还原的备份集”** 网格中，选择要还原的备份。 此网格将显示对于指定位置可用的备份。 默认情况下，系统会推荐一个恢复计划。 若要覆盖建议的恢复计划，可以更改网格中的选择。 当取消选择某个早期备份时，将自动取消选择那些需要还原该早期备份才能进行的备份。 有关“用于还原的备份集”网格中的列的信息，请参阅[还原数据库（“常规”页）](../../integration-services/general-page-of-integration-services-designers-options.md)。  
  
8.  或者单击 **“选择页”** 窗格中的 **“文件”** ，以便访问 **“文件”** 对话框。 在该对话框中，您可以通过在 **“将数据库文件还原为”** 网格中指定每个文件的新还原目标，将数据库还原到新的位置。 有关该网格的详细信息，请参阅[还原数据库（“文件”页）](restore-database-files-page.md)。  
  
9. 若要查看或选择高级选项，在 **“选项”** 页的 **“还原选项”** 面板中，可以根据您的实际情况选择下列任意选项：  
  
    1.  `WITH` 选项（不是必需的）：  
  
        -   **覆盖现有数据库(WITH REPLACE)**  
  
        -   **保留复制设置(WITH KEEP_REPLICATION)**  
  
        -   **限制对还原数据库的访问(WITH RESTRICTED_USER)**  
  
    2.  为 **“恢复状态”** 框选择一个选项。 此框确定还原操作之后的数据库状态。  
  
        -   **RESTORE WITH RECOVERY** 是默认行为，它通过回滚未提交的事务，使数据库处于可以使用的状态。 无法还原其他事务日志。 如果您要立即还原所有必要的备份，则选择此选项。  
  
        -   **RESTORE WITH NORECOVERY** 不对数据库执行任何操作，不回滚未提交的事务。 可以还原其他事务日志。 除非恢复数据库，否则无法使用数据库。  
  
        -   **RESTORE WITH STANDBY** 使数据库处于只读模式。 它撤消未提交的事务，但将撤消操作保存在备用文件中，以便能够还原恢复结果。  
  
    3.  如果对于选择的时间点是必需的，则选择“还原前进行结尾日志备份”。 无需修改此设置，但可以选择备份日志尾部（即使不需要）。 此处为文件名？ 如果 **“常规”** 页面中的每一个备份设置为 Windows Azure，则尾部日志也将备份到同一存储容器中。  
  
    4.  如果存在与数据库的活动连接，则还原操作可能会失败。 选中 **“关闭现有连接”** 以确保关闭 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 和数据库之间的所有活动连接。 此复选框可在执行还原操作之前将数据库设置为单用户模式，并在该操作完成后将数据库设置为多用户模式。  
  
    5.  如果要在每个还原操作之间进行提示，请选择 **“还原每个备份之前进行提示”** 。 除非数据库过大并且您要监视还原操作的状态，否则通常没有必要选中该选项。  
  
     有关这些还原选项的详细信息，请参阅 [还原数据库（“选项”页）](restore-database-options-page.md)），然后才能还原数据库。  
  
10. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [备份事务日志 (SQL Server)](back-up-a-transaction-log-sql-server.md)   
 [创建完整数据库备份 (SQL Server)](create-a-full-database-backup-sql-server.md)   
 [将数据库还原到新位置 (SQL Server)](restore-a-database-to-a-new-location-sql-server.md)   
 [还原事务日志备份 (SQL Server)](restore-a-transaction-log-backup-sql-server.md)   
 [RESTORE (Transact-SQL)](/sql/t-sql/statements/restore-statements-transact-sql)   
 [还原数据库（“选项”页）](restore-database-options-page.md)   
 [还原数据库（“常规”页）](../../integration-services/general-page-of-integration-services-designers-options.md)  
  
  
