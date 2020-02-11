---
title: 在对象资源管理器中管理事件会话 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xevents
ms.topic: conceptual
ms.assetid: 16849e38-d3fb-414d-8dcb-797b5ffce6ee
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d44ab9256367ceb9883b55bb9b01ad67e14ded32
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62705519"
---
# <a name="manage-event-sessions-in-the-object-explorer"></a>在对象资源管理器中管理事件会话
  本主题讨论您可以在 **“对象资源管理器”** 中执行的将影响扩展事件的操作：  
  
-   创建扩展事件会话  
  
-   开始或停止扩展事件会话  
  
-   导出扩展事件会话  
  
-   导入扩展事件会话模板  
  
-   编辑扩展事件会话  
  
-   删除扩展事件会话  
  
## <a name="create-an-extended-events-session"></a>创建扩展事件会话  
 有关创建扩展事件会话的详细信息，请参阅 [Create an Extended Events Session](../../database-engine/create-an-extended-events-session.md)。  
  
## <a name="starting-or-stopping-an-extended-events-session"></a>开始或停止扩展事件会话  
 您可以`ALTER EVENT SESSION`使用语句或使用**对象资源管理器**的 "**扩展事件**" 节点，通过**查询编辑器**启动或停止扩展事件会话。  
  
 在你停止某一事件会话后，该会话在 sys.dm_xe_sessions 动态管理视图 (DMV) 中不再作为活动会话列出。 但是，会话定义保持不变，并且您可以重新启动该会话。 若要完全删除某一会话定义，您必须删除该会话。  
  
 若要启动或停止扩展事件会话，您必须拥有 ALTER ANY EVENT SESSION 权限。  
  
 当你停止使用内存中目标（例如环形缓冲区、存储桶、事件配对或同步事件计数器目标）的会话时，在该会话的缓冲区中存储的所有信息（sys.dm_xe_session_targets DMV 的 target_data 列）将会丢失。 若要在停止该会话后访问事件数据，则应在停止该会话之前保存数据，或者配置该会话以使用文件目标。  
  
### <a name="start-or-stop-an-extended-events-session-using-query-editor"></a>使用查询编辑器启动或停止扩展事件会话  
 若要启用某一会话，请发出以下语句，使用扩展事件会话的名称替换 *session_name* ：  
  
```  
ALTER EVENT SESSION [session_name]  
ON SERVER  
STATE = START  
```  
  
 若要停止某一会话，请发出以下语句，使用扩展事件会话的名称替换 *session_name* ：  
  
```  
ALTER EVENT SESSION [session_name]  
ON SERVER  
STATE = STOP  
```  
  
### <a name="start-or-stop-an-extended-events-session-in-object-explorer"></a>在对象资源管理器中启动或停止扩展事件会话  
 若要在 **“对象资源管理器”** 中启动或停止扩展事件会话，则依次展开 **“管理”** 、 **“扩展事件”** 和“会话”  节点，右键单击所需的会话，然后单击 **“启动会话”** 或 **“停止会话”** 。  
  
## <a name="export-an-extended-events-session-template"></a>导出扩展事件会话模板  
 可以使用 **“对象资源管理器”** 导出扩展事件会话，并将它保存为 .xml 模板文件。 例如，您可能要导出会话，然后使用 **“新建会话向导”** 或 **“新建会话”** 对话框将模板应用到新的事件会话。  
  
 导出会话时，确保将模板文件保存到使用 NTFS 文件系统的某个位置，并且只允许有权查看该信息的用户对其进行访问。  
  
 在 **“对象资源管理器”** 中导出扩展事件会话：  
  
1.  依次展开 **“管理”** 、 **“扩展事件”** 和 **“会话”** 节点。  
  
2.  右键单击要导出的会话，然后选择“导出会话”  。  
  
3.  在 **“另存为”** 对话框中选择保存文件的位置，在 **“文件名”** 框中键入文件名，然后单击 **“保存”** 。  
  
     如果您将文件保存到默认的 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 模板位置，则当您使用 **“新建会话向导”** 和 **“新建会话”** 对话框时，该模板将出现在预定义模板的下拉列表中。  
  
## <a name="import-an-extended-events-session-template"></a>导入扩展事件会话模板  
 通过使用 **“对象资源管理器”** ，您可导入扩展事件会话的模板。 例如，您可能希望执行此操作以利用从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的其他实例导出的模板创建会话。  
  
 若要导入扩展事件会话，则您必须具有必要的 `ALTER ANY EVENT SESSION` 权限。  
  
 在您导入模板文件之前，确保该文件来自受信任的源。 应将模板文件保存到一个使用 NTFS 文件系统的位置，并限制只有获得授权查看信息的用户才可以访问该位置。  
  
 若要导入扩展事件会话：  
  
1.  在 **“对象资源管理器”** 中，依次展开 **“管理”** 和 **“扩展事件”** 节点。  
  
2.  右键单击“会话”  ，然后选择“新建会话”  。  
  
3.  指定会话的名称。  
  
4.  展开 **“模板”** 下拉框。  
  
5.  单击“**文件位置 …>打开”并通过浏览找到要导入的会话（XML 文件）\<** 。  
  
 会话将出现在 **“会话”** 节点下。 默认情况下，不会启动会话。  
  
## <a name="edit-an-extended-events-session"></a>编辑扩展事件会话  
 您可在“对象资源管理器”中编辑扩展事件会话。  
  
 编辑扩展事件会话：  
  
1.  在 **“对象资源管理器”** 中，依次展开 **“管理”** 、 **“扩展事件”** 和 **“会话”** 节点。  
  
2.  右键单击一个会话，然后选择“属性”  。  
  
3.  在 **“选择页”** 部分，选择您要编辑的页。  
  
4.  在完成对事件会话的修改后，单击 **“确定”** 。  
  
## <a name="script-an-event-session-definition-using-includetsqlincludestsql-mdmd"></a>使用 [!INCLUDE[tsql](../../includes/tsql-md.md)]  
 “新建会话向导”和“新建会话”对话框都包含一个可用于生成定义扩展事件会话的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的“脚本”选项。  
  
 可以通过以下方法访问现有扩展事件会话的 [!INCLUDE[tsql](../../includes/tsql-md.md)] ：右键单击该会话名称，选择 **“编写会话脚本为”** ，然后再选择 **“CREATE 到”** 。  
  
## <a name="delete-an-extended-events-session"></a>删除扩展事件会话  
 您可以删除扩展事件会话：  
  
-   在“查询编辑器”中使用 `DROP EVENT SESSION`。  
  
-   在 **“对象资源管理器”** 中。  
  
 在你删除某一事件会话时，所有配置信息都将被删除，并且会话定义不再在 sys.server_event_sessions 目录视图中出现。  
  
> [!NOTE]  
>  system_health 和 AlwaysOn_health 随一起[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]提供;不要删除它们。 默认情况下，将启用 system_health（有关详细信息，请参阅 [使用 system_health 会话](use-the-ssms-xe-profiler.md)）。 默认情况下，AlwaysOn_health 处于关闭状态。 这些会话将收集可用于诊断性能问题的数据。  
  
 若要删除某一扩展事件会话，您必须具有 ALTER ANY EVENT SESSION 权限。  
  
 若要在 **“对象资源管理器”** 中删除扩展事件会话：  
  
1.  依次展开 **“管理”** 、 **“扩展事件”** 和 **“会话”** 节点。  
  
2.  右键单击一个会话，然后选择“删除”  。  
  
3.  在 **“删除对象”** 对话框中，单击 **“确定”** 。  
  
4.  在完成对事件会话的修改后，单击 **“确定”** 。  
  
 若要在“查询编辑器”  中删除一个扩展事件会话，请发出以下语句，并将 *session_name* 替换为你要删除的扩展事件会话的名称：  
  
```  
DROP EVENT SESSION [session_name]  
ON SERVER  
```  
  
  
