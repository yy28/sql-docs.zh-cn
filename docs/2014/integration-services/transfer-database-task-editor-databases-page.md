---
title: 传输数据库任务编辑器（"数据库" 页） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferdatabasetask.database.f1
helpviewer_keywords:
- Transfer Database Task Editor
ms.assetid: ccdb74d0-4bea-420c-a726-2e0eb8957e0a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8d93d2e95f6a18174a6d9b2f05e434a5443701ed
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66055113"
---
# <a name="transfer-database-task-editor-databases-page"></a>传输数据库任务编辑器（“数据库”页）
  使用 **“传输数据库任务编辑器”** 对话框的 **“数据库”** 页可为传输数据库任务涉及的源数据库和目标数据库指定属性。 传输数据库任务将在两个 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例之间复制或移动 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]数据库。 此任务还可以用来复制同一个服务器上的数据库。 有关此任务的详细信息，请参阅 [传输数据库任务](control-flow/transfer-database-task.md)。  
  
## <a name="options"></a>选项  
 **SourceConnection**  
 在列表中选择一个 SMO 连接管理器，或单击** \<"新建连接 ..." >** 以创建与源服务器的新连接。  
  
 **DestinationConnection**  
 在列表中选择一个 SMO 连接管理器，或单击** \<"新建连接 ..." >** 以创建与目标服务器的新连接。  
  
 **DestinationDatabaseName**  
 指定目标服务器上的 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 数据库的名称。  
  
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
  
|值|说明|  
|-----------|-----------------|  
|**True**|覆盖目标服务器数据库。|  
|**False**|不覆盖目标服务器数据库。|  
  
> [!CAUTION]  
>  如果为 **DestinationOverwrite** 指定 **True**，则会覆盖目标服务器数据库中的数据，这可能导致数据丢失。 若要避免数据丢失，请在执行传输数据库任务之前将目标服务器数据库备份到其他位置。  
  
 **Action**  
 指定该任务是将数据库“复制”到目标服务器还是“移动”到目标服务器********。  
  
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
  
|值|说明|  
|-----------|-----------------|  
|**True**|重新附加源数据库。|  
|**False**|不重新附加源数据库。|  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services 错误和消息引用](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Integration Services 任务](control-flow/integration-services-tasks.md)   
 [传输数据库任务编辑器 &#40;常规 "页面&#41;](general-page-of-integration-services-designers-options.md)   
 [“表达式”页](expressions/expressions-page.md)   
 [SMO 连接管理器](connection-manager/smo-connection-manager.md)  
  
  
