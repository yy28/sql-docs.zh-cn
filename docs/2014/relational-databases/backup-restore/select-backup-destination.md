---
title: 选择备份目标 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.selectbackupdest.f1
ms.assetid: f79e824b-1525-45de-8ede-513563af41b6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d9b4a0e07f32e074ff7e8875c263615bcebc12d1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62874881"
---
# <a name="select-backup-destination"></a>选择备份目标
  使用 **“选择备份目标”** 对话框可以选择一个设备作为备份目标。 备份目标可以是磁盘，也可以是逻辑备份设备。  
  
 **使用 SQL Server Management Studio 备份数据库**  
  
-   [创建完整数据库备份 (SQL Server)](create-a-full-database-backup-sql-server.md)  
  
-   [创建差异数据库备份 (SQL Server)](create-a-differential-database-backup-sql-server.md)  
  
-   [备份文件和文件组 (SQL Server)](back-up-files-and-filegroups-sql-server.md)  
  
-   [备份事务日志 (SQL Server)](back-up-a-transaction-log-sql-server.md)  
  
## <a name="options"></a>选项  
 此对话框中的选项取决于所选目标是位于磁盘上还是位于磁带上。  
  
 **磁盘上的目标**  
 若要指定备份目标，请选择下列选项之一。  
  
|||  
|-|-|  
|**文件名**|选择此选项，以在文本框中输入作为备份目标的本地文件或远程文件。<br /><br /> 若要指定本地文件，单击文本框右侧的浏览按钮并导航到运行服务器的计算机的固定驱动器上的文件或直接; 输入完整路径和文件名例如， `C:\Program Files\Microsoft SQL Server\MSSQL\Backup\AdventureWorksBackup.bak`。<br /><br /> 若要将远程文件指定为备份目标，请输入其完全限定的通用命名约定 (UNC) 名称。 有关详细信息，请参阅 [备份设备 (SQL Server)](backup-devices-sql-server.md)。<br /><br /> **\*\* 重要说明 \*\*** 通过网络备份数据时可能会出现网络错误；因此，建议你在完成备份后验证备份操作。 有关详细信息，请参阅 [RESTORE VERIFYONLY (Transact-SQL)](/sql/t-sql/statements/restore-statements-verifyonly-transact-sql)。|  
|**备份设备**|选择此选项以选择逻辑备份设备。<br /><br /> 注意：有关如何创建磁盘备份设备的信息，请参阅[为磁盘文件定义逻辑备份设备&#40;SQL Server&#41;](define-a-logical-backup-device-for-a-disk-file-sql-server.md)。|  
  
 **磁带上的目标**  
 在与运行服务器（即 [!INCLUDE[ssDE](../../includes/ssde-md.md)]的实例）的计算机建立了物理连接的磁带机上指定备份目标。 选择以下选项之一：  
  
|||  
|-|-|  
|**磁带机**|选择此选项，以从与运行服务器实例的计算机建立了物理连接的磁带机列表中选择磁带机作为备份目标。<br /><br /> 注意：远程计算机中的磁带备份设备不是有效的备份目标。|  
|**备份设备**|选择此选项以选择现有的逻辑备份设备。 这些逻辑备份设备对应于与运行服务器实例的计算机建立了物理连接的磁带机。<br /><br /> 注意：有关如何创建磁带备份设备的信息，请参阅[为磁带机定义逻辑备份设备&#40;SQL Server&#41;](define-a-logical-backup-device-for-a-tape-drive-sql-server.md)。|  
  
## <a name="see-also"></a>请参阅  
 [备份设备 (SQL Server)](backup-devices-sql-server.md)   
 [媒体集、媒体簇和备份集 (SQL Server)](media-sets-media-families-and-backup-sets-sql-server.md)  
  
  
