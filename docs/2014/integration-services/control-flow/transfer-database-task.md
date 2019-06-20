---
title: 传输数据库任务 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferdatabasetask.f1
helpviewer_keywords:
- Transfer Database task [Integration Services]
ms.assetid: b9a2e460-cdbc-458f-8df8-06b8b2de3d67
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f7ddf838269932c19b0614d5a5219a7f03daed17
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62830146"
---
# <a name="transfer-database-task"></a>传输数据库任务
  传输数据库任务在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的两个实例之间传输 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库。 与只通过复制方式传输 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对象的其他任务相比，传输数据库任务既可以复制也可以移动数据库。 此任务还可以用来复制同一个服务器上的数据库。  
  
## <a name="offline-and-online-modes"></a>脱机和联机模式  
 可以使用联机模式或脱机模式传输数据库。 在使用联机模式时，数据库保持连接的情况下，通过使用 SQL 管理对象 (SMO) 复制数据库对象来传输数据库。 在使用脱机模式时，数据库断开连接，然后复制或移动数据库文件，在传输成功完成后，数据库连接到目标服务器。 如果是复制数据库，则在复制成功后，数据库自动与源服务器重新连接。 在脱机模式中，复制数据库的速度会快一些，但在传输过程中用户无法使用该数据库。  
  
 脱机模式要求您在源服务器和目标服务器上指定包含数据库文件的网络文件共享。 如果共享了该文件夹且用户可以访问它，则可以使用语法 \\\computername\Program Files\myfolder\\来引用该网络共享。 否则，必须使用语法 \\\computername\c$\Program Files\myfolder\\。 若要使用后一种语法，用户必须对源和目标网络共享具有写权限。  
  
## <a name="transfer-of-databases-between-versions-of-sql-server"></a>在不同版本的 SQL Server 之间传输数据库  
 传输数据库任务可在不同 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本的实例之间传输数据库。  
  
## <a name="events"></a>事件  
 传输数据库任务并不报告错误消息传输的进度，它仅报告 0% 和 100 % 完成。  
  
## <a name="execution-value"></a>执行值  
 在该任务的 `ExecutionValue` 属性中定义的执行值返回值 1，因为与其他传输任务相比，传输数据库任务只能传输一个数据库。  
  
 通过将用户定义变量分配给传输数据库任务的 `ExecValueVariable` 属性，包中的其他对象就可以访问有关错误消息传输的信息。 有关详细信息，请参阅 [Integration Services (SSIS) 变量](../integration-services-ssis-variables.md)和[在包中使用变量](../use-variables-in-packages.md)。  
  
## <a name="log-entries"></a>日志项  
 传输数据库任务包括下列自定义日志项：  
  
-   SourceSQLServer   此日志项列出源服务器的名称。  
  
-   DestSQLServer   此日志项列出目标服务器的名称。  
  
-   SourceDB   此日志项列出已传输的数据库的名称。  
  
 此外，在覆盖目标数据库时会写入 `OnInformation` 事件的日志项。  
  
## <a name="security-and-permissions"></a>安全性和权限  
 若要使用脱机模式传输数据库，运行包的用户必须是 sysadmin 服务器角色的成员。  
  
 若要使用联机模式传输数据库，运行包的用户必须是 sysadmin 服务器角色的成员或所选数据库的数据库所有者 (dbo)。  
  
## <a name="configuration-of-the-transfer-database-task"></a>传输数据库任务的配置  
 您可以指定该任务是否在源数据库传输失败后尝试重新连接该数据库。  
  
 传输数据库任务还可以配置为允许覆盖同名的目标数据库，也就是替换目标数据库。  
  
 源数据库也可以在传输过程中重命名。 如果要将数据库传输到已经包含同名数据库的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的目标实例，则可以重命名源数据库，以允许传输该数据库。 但是，数据库文件名也必须不同；如果同名数据库文件已经存在于目标实例上，则该任务将失败。  
  
 复制数据库时，数据库不能比目标服务器上的 **模型** 数据库小。 可以增加要复制的数据库的大小，也可以减小 **模型**数据库的大小。  
  
 在运行时，传输数据库任务使用一个或多个 SMO 连接管理器连接到源服务器和目标服务器。 在同一服务器上创建数据库的副本时，只需要一个 SMO 连接管理器。 SMO 连接管理器与传输数据库任务分开进行配置，然后在传输数据库任务中引用连接管理器。 SMO 连接管理器指定在该任务访问服务器时使用的服务器和身份验证模式。 有关详细信息，请参阅 [SMO Connection Manager](../connection-manager/smo-connection-manager.md)。  
  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式来设置属性。  
  
 有关可以在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请单击下列主题之一：  
  
-   [传输数据库任务编辑器（“常规”页）](../general-page-of-integration-services-designers-options.md)  
  
-   [传输数据库任务编辑器（“数据库”页）](../transfer-database-task-editor-databases-page.md)  
  
-   [“表达式”页](../expressions/expressions-page.md)  
  
 有关如何在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置这些属性的详细信息，请单击下列主题：  
  
-   [设置任务或容器的属性](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="programmatic-configuration-of-the-transfer-database-task"></a>传输数据库任务的编程配置  
 有关以编程方式设置这些属性的详细信息，请单击以下主题：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferDatabaseTask.TransferDatabaseTask>  
  
  
