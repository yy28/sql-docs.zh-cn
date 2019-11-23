---
title: 备份数据库（“常规”页）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.backupdatabase.general.f1
ms.assetid: 5c344dfd-1ad3-41cc-98cd-732973b4a162
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: fc6680702fd32c670d2f3c3861c47bab96c52c47
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155074"
---
# <a name="back-up-database-general-page"></a>备份数据库（“常规”页）
  使用 **“备份数据库”** 对话框中的 **“常规”** 页可以查看或修改数据库备份操作的设置。  
  
 有关基本备份概念的详细信息，请参阅 [备份概述 (SQL Server)](backup-overview-sql-server.md)。  
  
> [!NOTE]  
>  使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 指定备份任务时，可以通过单击“脚本”[!INCLUDE[tsql](../../includes/tsql-md.md)][按钮，再为脚本选择一个目标，生成对应的 ](/sql/t-sql/statements/backup-transact-sql)**BACKUP** 脚本。  
  
 **使用 SQL Server Management Studio 创建备份**  
  
-   [创建完整数据库备份 (SQL Server)](create-a-full-database-backup-sql-server.md)  
  
-   [创建差异数据库备份 (SQL Server)](create-a-differential-database-backup-sql-server.md)  
  
    > [!IMPORTANT]  
    >  可以定义用于创建数据库备份的数据库维护计划。 有关详细信息，请参阅 [联机丛书中的](../maintenance-plans/maintenance-plans.md) 数据库维护计划 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 。  
  
 **创建部分备份**  
  
-   对于部分备份，必须使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] [BACKUP](/sql/t-sql/statements/backup-transact-sql) 语句和 PARTIAL 选项。  
  
## <a name="options"></a>“常规”  
  
### <a name="source"></a>Source  
 可通过 **“源”** 面板中的选项标识数据库并指定备份操作的备份类型和组件。  
  
 **“数据库”**  
 选择要备份的数据库。  
  
 **恢复模式**  
 查看为所选数据库显示的恢复模式（SIMPLE、FULL 或 BULK_LOGGED）。  
  
 **备份类型**  
 选择要对指定数据库执行的备份的类型。  
  
|备份类型|适用于|限制|  
|-----------------|-------------------|------------------|  
|Full|数据库、文件和文件组|对于 **master** 数据库，只能执行完整备份。<br /><br /> 在简单恢复模式下，文件和文件组备份只适用于只读文件组。|  
|差异|数据库、文件和文件组|在简单恢复模式下，文件和文件组备份只适用于只读文件组。|  
|事务日志|事务日志|事务日志备份不适用于简单恢复模式。|  
  
 **仅复制备份**  
 选择创建仅复制备份。 *仅复制备份* 是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 独立于常规备份序列 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的备份。 有关详细信息，请参阅[仅复制备份 (SQL Server)](copy-only-backups-sql-server.md)。  
  
> [!NOTE]  
>  选择“差异”选项时，无法创建仅复制备份。  
  
 **备份组件**  
 选择要备份的数据库组件。 如果在 **“备份类型”** 列表中选择了 **“事务日志”** ，则不会激活此选项。  
  
 选择以下选项按钮之一：  
  
|||  
|-|-|  
|**“数据库”**|指定备份整个数据库。|  
|**文件和文件组**|指定要备份的文件和/或文件组。<br /><br /> 选择此选项，打开 **“选择文件和文件组”** 对话框。 在选择要备份的文件组或文件并单击“确定”后，所选内容将显示在“文件组和文件” 框中。|  
  
### <a name="destination"></a>目标  
 “目标” 面板中的选项允许您为备份操作指定备份设备的类型，并查找现有的逻辑或物理备份设备。  
  
> [!NOTE]  
>  有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 备份设备的信息，请参阅[备份设备 (SQL Server)](backup-devices-sql-server.md)。  
  
 **备份到**  
 选择以下类型介质之一，作为要备份到的目标。 选择的目标将显示在 **“备份到”** 列表中。  
  
|||  
|-|-|  
|**磁盘**|备份到磁盘。 这可能是一个为该数据库创建的系统文件或基于磁盘的逻辑备份设备。 当前所选的磁盘将显示在 **“备份到”** 列表中。 您最多可以为备份操作选择 64 个磁盘设备。|  
|**磁带**|备份到磁带。 这可能是一个为该数据库创建的本地磁带机或基于磁带的逻辑备份设备。 当前所选的磁带将显示在 **“备份到”** 列表中。 最大数目为 64。 如果服务器没有相连的磁带设备，此选项将停用。 您选择的磁带将列在 **“备份到”** 列表中。<br /><br /> 注意：在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的未来版本中将不再支持磁带备份设备。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。|  
|**URL**|备份到 Azure Blob 存储。|  
  
 显示的下一组选项会取决于所选目标的类型。 如果您选择“磁盘”或“磁带”，则会显示以下选项。  
  
 **添加**  
 将文件或设备添加到“备份到”列表中。 最多可以同时向本地磁盘或远程磁盘上的 64 个设备进行备份。 若要指定远程磁盘上的文件，请使用完全限定的通用命名约定 (UNC) 名称。 有关详细信息，请参阅 [备份设备 (SQL Server)](backup-devices-sql-server.md)实例的计算机附连有磁带机时，此选项才可用。  
  
 **删除**  
 从“备份到”列表中删除一个或多个当前所选的设备。  
  
 **目录**  
 显示所选设备的介质内容。  
  
 如果您选择“URL”作为备份目标，则会显示以下选项：  
  
 **文件名**  
 指定备份文件的名称。  
  
 **SQL 凭据**  
 选择用于向 Azure 存储进行身份验证的 SQL 凭据。 如果没有可使用的现有 SQL 凭据，则单击 **“创建”** 按钮可创建新的 SQL 凭据。  
  
> [!IMPORTANT]  
>  单击 **“创建”** 打开的对话框需要管理证书或订阅的发布配置文件。 如果您无权访问管理证书或发布配置文件，可以创建一个 SQL 凭据，方法是使用 Transact-SQL 或 SQL Server Management Studio 指定存储帐户名称和访问密钥信息。 请参阅[创建凭据](../security/authentication-access/create-a-credential.md#Credential)主题中中的示例代码，使用 transact-sql 创建凭据。 或者，使用 SQL Server Management Studio，从数据库引擎实例中右键单击 **“安全性”** ，依次选择 **“新建”** 和 **“凭据”** 。 在 **“标识”** 字段中指定存储帐户名称，在 **“密码”** 字段中指定访问密钥。  
  
 **Azure 存储容器**  
 指定 Azure 存储容器的名称  
  
 **URL 前缀：**  
 这是基于在 SQL 凭据中存储的存储帐户信息以及您指定的 Azure 存储容器名称自动生成的。 我们建议你不要编辑此字段中的信息，除非你使用的域采用 **\<存储帐户>.blob.core.windows.net** 以外的格式。  
  
## <a name="see-also"></a>另请参阅  
 [备份事务日志 (SQL Server)](back-up-a-transaction-log-sql-server.md)   
 [备份文件和文件组 (SQL Server)](back-up-files-and-filegroups-sql-server.md)   
 [为磁盘文件定义逻辑备份设备 (SQL Server)](define-a-logical-backup-device-for-a-disk-file-sql-server.md)   
 [为磁带驱动器定义逻辑备份设备 (SQL Server)](define-a-logical-backup-device-for-a-tape-drive-sql-server.md)   
 [恢复模式 (SQL Server)](recovery-models-sql-server.md)  
  
  
