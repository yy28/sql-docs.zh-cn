---
title: “备份数据库”任务（维护计划）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql12.swb.maint.backup.f1
- sql12.swb.maint.maintplanproperties.logbackup.f1
helpviewer_keywords:
- Back Up Database Task dialog box
ms.assetid: ed1ef012-fa14-4ba5-bafe-d1527ba065b3
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4a31052bb0633d370098e328741432f6b854d65e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68205945"
---
# <a name="back-up-database-task-maintenance-plan"></a>“备份数据库”任务（维护计划）
  使用 "**备份数据库任务**" 对话框可以将备份任务添加到维护计划。 备份数据库非常重要，因为当发生系统或硬件故障（或用户错误）对数据库造成某种破坏时，就需要用备份副本来还原数据。 此任务可用于执行完整备份、差异备份、文件和文件组备份以及事务日志备份。  
  
 **创建备份数据库任务**  
  
-   [创建维护计划](create-a-maintenance-plan.md)  
  
## <a name="options"></a>选项  
 **连接**  
 选择执行此任务时使用的服务器连接。  
  
 **新建**  
 创建一个新的服务器连接，在执行此任务时使用。 下面对 **“新建连接”** 对话框进行了介绍。  
  
 **数据库**  
 指定受此任务影响的数据库。 选择此选项时，此下拉列表会提供以下选项： **“所有数据库”**、 **“所有系统数据库”**、 **“所有用户数据库”** 和 **“特定数据库”**。  
  
 **所有数据库**  
 生成的维护计划将对所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库运行维护任务。  
  
 **所有系统数据库（master、msdb、model）**  
 生成的维护计划将对每个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统数据库运行维护任务。 对用户创建的数据库不运行维护任务。  
  
 **所有用户数据库（master、model、msdb、tempdb 除外）**  
 生成的维护计划将对用户创建的所有数据库运行维护任务。 但不会对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统数据库运行任何维护任务。  
  
 **这些数据库**  
 生成的维护计划将只对所选数据库运行维护任务。 如果选择此选项，则必须至少在列表中选择一个数据库。  
  
 **备份类型**  
 显示要执行的备份类型。  
  
 **备份组件**  
 选择“数据库”**** 将备份整个数据库。 选择 **“文件和文件组”** 将只备份部分数据库。 如果选择此选项，请提供文件或文件组名称。 如果在 **“数据库”** 框中选择了多个数据库，只能对 **“备份组件”** 指定 **“数据库”**。 若要执行文件或文件组备份，请为每个数据库创建一个任务。  
  
 **备份集过期时间**  
 指定可用其他备份集覆盖此备份集的时间。  
  
 **备份到**  
 将数据库备份到文件或磁带。 只有连接到该数据库所在计算机的磁带设备才可用。  
  
 **跨一个或多个文件备份数据库**  
 单击“添加”**** 将打开“选择备份目标”**** 对话框，并提供一个或多个磁盘位置，或磁带设备。  
  
 **如果备份文件存在**  
 选择“追加”**** 可以将此备份添加到文件的末尾。 选择 **“覆盖”** 可以删除文件中的任意旧备份，并用此新备份替换它们。  
  
 **为每个数据库创建备份文件**  
 在文件夹框中指定的位置创建一个备份文件。 将为选定的每个数据库创建一个文件。  
  
 **为每个数据库创建子目录**  
 选择此选项可以将每个数据库置于一个子文件夹中。  
  
> [!IMPORTANT]  
>  尽管维护计划可以创建子目录，但维护任务不能删除子目录。 此功能减少了使用清除维护任务删除文件的恶意攻击的可能性。  
  
> [!IMPORTANT]  
>  此子目录将从父目录中继承权限。 请限制相关权限，以避免未经授权的访问。  
  
 **文件夹**  
 指定用来放置自动创建的数据库文件的文件夹。  
  
 **备份文件扩展名**  
 指定备份文件要使用的扩展名。 默认为 **.bak**。  
  
 **验证备份完整性**  
 验证备份集是否完整以及所有卷是否都可读。  
  
 **备份日志尾部，并使数据库处于还原状态**  
 在还原数据库前，执行作为最后一个步骤的日志备份。 有关详细信息，请参阅[结尾日志备份 (SQL Server)](../backup-restore/tail-log-backups-sql-server.md)。  
  
 **设置备份压缩**  
 在 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] （或更高版本）中，选择以下 [备份压缩](../backup-restore/backup-compression-sql-server.md) 值之一：  
  
|||  
|-|-|  
|**使用默认服务器设置**|单击此选项可使用服务器级别默认值。<br /><br /> 此默认值可通过 **backup compression default** 服务器配置选项进行设置。 有关如何查看此选项的当前设置的信息，请参阅[查看或配置备份压缩默认服务器配置选项](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)。|  
|**压缩备份**|单击此选项可压缩备份，而不考虑服务器级别默认值。<br /><br /> ** \* \*重要\*提示**默认情况下，压缩会显著增加 CPU 使用率，并且压缩进程占用的额外 CPU 可能会对并发操作造成不利影响。 因此，你可能需要在会话中创建低优先级的压缩备份，其 CPU 使用率受 [资源调控器](../resource-governor/resource-governor.md)限制。 有关详细信息，请参阅本主题后面的 [使用资源调控器限制备份压缩的 CPU 使用量 (Transact-SQL)](../backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)限制。|  
|**不压缩备份**|单击此选项可创建未压缩的备份，而不考虑服务器级别默认值。|  
  
 **查看 T-sql**  
 根据所选选项，查看针对此任务的服务器执行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。  
  
> [!NOTE]  
>  当受影响的对象很多时，可能需要相当长的时间才可显示。  
  
## <a name="new-connection-dialog-box"></a>“新建连接”对话框  
 **连接名称**  
 输入新连接的名称。  
  
 **选择或输入服务器名称**  
 选择执行此任务时所要连接的服务器。  
  
 **“刷新”**  
 刷新可用服务器的列表。  
  
 **输入用于登录到服务器的信息**  
 指定如何对服务器进行身份验证。  
  
 **使用 Windows 集成安全性**  
 使用 Windows 身份验证连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的实例。  
  
 **使用特定的用户名和密码**  
 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 身份验证连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例。 此选项不可用。  
  
 **用户名**  
 提供一个在进行身份验证时要使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名。 此选项不可用。  
  
 **权限**  
 提供一个在进行身份验证时要使用的密码。 此选项不可用。  
  
## <a name="see-also"></a>另请参阅  
 [BACKUP (Transact-SQL)](/sql/t-sql/statements/backup-transact-sql)  
  
  
