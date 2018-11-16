---
title: 传输数据库任务 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.transferdatabasetask.f1
- sql13.dts.designer.transferdatabasetask.general.f1
- sql13.dts.designer.transferdatabasetask.database.f1
- sql13.dts.designer.transferdatabasetask.sourcedbfiles.f1
- sql13.dts.designer.transferdatabasetask.destdbfiles.f1
helpviewer_keywords:
- Transfer Database task [Integration Services]
ms.assetid: b9a2e460-cdbc-458f-8df8-06b8b2de3d67
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2492d80cd8899002d0b6baf5c219b5a724a6aab9
ms.sourcegitcommit: 0638b228980998de9056b177c83ed14494b9ad74
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/14/2018
ms.locfileid: "51639074"
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
 在该任务的 **ExecutionValue** 属性中定义的执行值返回值 1，因为与其他传输任务相比，传输数据库任务只能传输一个数据库。  
  
 通过将用户定义的变量分配给传输数据库任务的 **ExecValueVariable** 属性，包中的其他对象就可以访问有关错误消息传输的信息。 有关详细信息，请参阅 [Integration Services (SSIS) 变量](../../integration-services/integration-services-ssis-variables.md)和[在包中使用变量](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)。  
  
## <a name="log-entries"></a>日志项  
 传输数据库任务包括下列自定义日志项：  
  
-   SourceSQLServer   此日志项列出源服务器的名称。  
  
-   DestSQLServer   此日志项列出目标服务器的名称。  
  
-   SourceDB   此日志项列出已传输的数据库的名称。  
  
 此外，在覆盖目标数据库时会写入 **OnInformation** 事件的日志项。  
  
## <a name="security-and-permissions"></a>安全性和权限  
 若要使用脱机模式传输数据库，运行包的用户必须是 sysadmin 服务器角色的成员。  
  
 若要使用联机模式传输数据库，运行包的用户必须是 sysadmin 服务器角色的成员或所选数据库的数据库所有者 (dbo)。  
  
## <a name="configuration-of-the-transfer-database-task"></a>传输数据库任务的配置  
 您可以指定该任务是否在源数据库传输失败后尝试重新连接该数据库。  
  
 传输数据库任务还可以配置为允许覆盖同名的目标数据库，也就是替换目标数据库。  
  
 源数据库也可以在传输过程中重命名。 如果要将数据库传输到已经包含同名数据库的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的目标实例，则可以重命名源数据库，以允许传输该数据库。 但是，数据库文件名也必须不同；如果同名数据库文件已经存在于目标实例上，则该任务将失败。  
  
 复制数据库时，数据库不能比目标服务器上的 **模型** 数据库小。 可以增加要复制的数据库的大小，也可以减小 **模型**数据库的大小。  
  
 在运行时，传输数据库任务使用一个或多个 SMO 连接管理器连接到源服务器和目标服务器。 在同一服务器上创建数据库的副本时，只需要一个 SMO 连接管理器。 SMO 连接管理器与传输数据库任务分开进行配置，然后在传输数据库任务中引用连接管理器。 SMO 连接管理器指定在该任务访问服务器时使用的服务器和身份验证模式。 有关详细信息，请参阅 [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md)。  
  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器或以编程方式设置属性。  
  
 有关可在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请单击以下主题：  
  
-   [“表达式”页](../../integration-services/expressions/expressions-page.md)  
  
 有关如何在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置这些属性的详细信息，请单击下列主题：  
  
-   [设置任务或容器的属性](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-transfer-database-task"></a>传输数据库任务的编程配置  
 有关以编程方式设置这些属性的详细信息，请单击以下主题：  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferDatabaseTask.TransferDatabaseTask>  
  
## <a name="transfer-database-task-editor-general-page"></a>传输数据库任务编辑器（“常规”页）
  使用 **“传输数据库任务编辑器”** 对话框的 **“常规”** 页，可以对传输数据库任务进行命名和说明。 传输数据库任务将在两个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例之间复制或移动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库。 此任务还可以用来复制同一个服务器上的数据库。   
  
### <a name="options"></a>选项  
 **名称**  
 为传输数据库任务键入唯一的名称。 此名称用作任务图标中的标签。  
  
> [!NOTE]  
>  任务名称在一个包内必须是唯一的。  
  
 **Description**  
 键入传输数据库任务的说明。  
  
## <a name="transfer-database-task-editor-databases-page"></a>传输数据库任务编辑器（“数据库”页）
  使用 **“传输数据库任务编辑器”** 对话框的 **“数据库”** 页可为传输数据库任务涉及的源数据库和目标数据库指定属性。 传输数据库任务将在两个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例之间复制或移动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库。 此任务还可以用来复制同一个服务器上的数据库。  
  
### <a name="options"></a>选项  
 **SourceConnection**  
 从列表中选择 SMO 连接管理器，或单击“\<新建连接...>”，创建与源服务器的新连接。  
  
 **DestinationConnection**  
 从列表中选择 SMO 连接管理器，或单击“\<新建连接...>”，创建与目标服务器的新连接。  
  
 **DestinationDatabaseName**  
 指定目标服务器上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库的名称。  
  
 若要使用源数据库名称自动填充此字段，请首先指定 **SourceConnection** 和 **SourceDatabaseName** 。  
  
 若要重命名目标服务器上的数据库，请在此字段中键入新名称。  
  
 **DestinationDatabaseFiles**  
 指定目标服务器上数据库文件的名称和位置。  
  
 若要使用源数据库文件的名称和位置自动填充此字段，请首先指定 **SourceConnection**、 **SourceDatabaseName**和 **SourceDatabaseFiles** 。  
  
 若要对目标服务器上的数据库文件进行重命名或为其指定新位置，请使用源数据库信息填充此字段，再单击浏览按钮。 在 **“目标数据库文件”** 对话框中，编辑 **“目标文件”**、 **“目标文件夹”** 或 **“网络文件共享”**。  
  
> [!NOTE]  
>  如果使用浏览按钮来定位数据库文件，则会使用本地驱动器表示法输入文件位置：例如，c:\\。 您必须将其替换为网络共享表示法（包括计算机名称和共享名称）。 如果使用默认的管理共享，您必须使用 $ 表示法，并且必须具有对该共享位置的管理权限。  
  
 **DestinationOverwrite**  
 指定是否可以覆盖目标服务器上的数据库。  
  
 此属性具有下表所列的选项：  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**True**|覆盖目标服务器数据库。|  
|**False**|不覆盖目标服务器数据库。|  
  
> [!CAUTION]  
>  如果为 **DestinationOverwrite** 指定 **True**，则会覆盖目标服务器数据库中的数据，这可能导致数据丢失。 若要避免数据丢失，请在执行传输数据库任务之前将目标服务器数据库备份到其他位置。  
  
 **操作**  
 指定该任务是将数据库“复制”到目标服务器还是“移动”到目标服务器。  
  
 **方法**  
 指定是在源服务器上的数据库处于在线模式时执行任务还是在其处于离线模式时执行任务。  
  
 若要使用离线模式传输数据库，运行包的用户必须是 **sysadmin** 固定服务器角色的成员。  
  
 若要使用在线模式传输数据库，运行包的用户必须是 **sysadmin** 固定服务器角色的成员或是所选数据库的数据库所有者 (**dbo**)。  
  
 **SourceDatabaseName**  
 选择要复制或移动的数据库的名称。  
  
 **SourceDatabaseFiles**  
 单击浏览按钮来选择数据库文件。  
  
 **ReattachSourceDatabase**  
 指定在发生错误时该任务是否将尝试重新附加源数据库。  
  
 此属性具有下表所列的选项：  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**True**|重新附加源数据库。|  
|**False**|不重新附加源数据库。|  

## <a name="source-database-files"></a>源数据库文件
  可以使用 **“源数据库文件”** 对话框查看源服务器上的数据库文件的名称和位置，或者为传输数据库任务指定网络文件共享位置。   
  
 若要使用源服务器上数据库文件的名称和位置填充此对话框，请首先在 **“传输数据库任务编辑器”** 对话框的 **“数据库”** 页中指定 **SourceConnection** 和 **SourceDatabaseName** 。  
  
### <a name="options"></a>选项  
 **源文件**  
 源服务器上要传输的数据库文件的名称。 **“源文件”** 是只读的。  
  
 **源文件夹**  
 源服务器上包含要传输的数据库文件的文件夹。 **“源文件夹”** 是只读的。  
  
 **网络文件共享**  
 源服务器上要从中传输数据库文件的网络共享文件夹。 通过在 **“传输数据库任务编辑器”** 对话框的 **“数据库”** 页中为 **“方法”** 指定 **DatabaseOffline** 以脱机模式传输数据库时，可以使用 **“网络文件共享”** 。  
  
 输入网络文件共享位置，或单击浏览按钮 **(…)** 可查找网络文件共享位置。  
  
 以脱机模式传输数据库时，数据库文件在传输到目标服务器之前将被复制到源服务器上的 **“网络文件共享”** 位置。  

## <a name="destination-database-files"></a>目标数据库文件
  可以使用 **“目标数据库文件”** 对话框查看或更改目标服务器上的数据库文件的名称和位置，或为传输数据库任务指定网络文件位置。  
  
 若要使用源服务器上数据库文件的名称和位置自动填充此对话框，请首先在 **“传输数据库任务编辑器”** 对话框的 **“数据库”** 页中指定 **SourceConnection** 、 **SourceDatabaseName** 和 **SourceDatabaseFiles** 。  
  
### <a name="options"></a>选项  
 **目标文件**  
 目标服务器上作为传输目标的数据库文件的名称。  
  
 请输入文件名，或单击文件名以编辑该名称。  
  
 **目标文件夹**  
 数据库文件要传输到的目标服务器上的文件夹。  
  
 请输入文件夹路径，单击文件夹路径以编辑该路径，或单击“浏览”以找到数据库文件要传输到的目标服务器上的文件夹。  
  
 **网络文件共享**  
 数据库文件要传输到的目标服务器上的网络共享文件夹。 通过在 **“传输数据库任务编辑器”** 对话框的 **“数据库”** 页中为 **“方法”** 指定 **DatabaseOffline** 以脱机模式传输数据库时，可以使用 **“网络文件共享”** 。  
  
 请输入网络文件共享位置，或单击“浏览”以找到网络文件共享位置。  
  
 以脱机模式传输数据库时，数据库文件先复制到 **“网络文件共享”** 位置，然后才会传输到 **“目标文件夹”** 位置。  
