---
title: 使用 SQL Server 扩展事件监视 Analysis Services |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 616cc1e633d6683283d62d6fb3b3434780d9a919
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/26/2018
ms.locfileid: "50147242"
---
# <a name="monitor-analysis-services-with-sql-server-extended-events"></a>使用 SQL Server 扩展事件监视 Analysis Services
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas-all-aas.md)]
  扩展事件 (xEvents) 是一种占用系统资源非常少的轻量跟踪和性能监视系统，因此成为诊断生产和测试服务器问题的理想工具。 它还是高度可扩展、可配置的，且位于 SQL Server 2016 中，可通过新的内置工具支持更轻松地使用。 在 SQL Server Management Studio 中，连接到 Analysis Services 实例后，你可配置、运行及监视实时跟踪，类似于使用 SQL Server Profiler。 添加了更好的工具应使 xEvents 成为 SQL Server Profiler 更合理的替代，并且在如何诊断数据库引擎问题和 Analysis Services 工作负荷问题中创建更多对称。  
  
 除了 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，还可以通过 XMLA 脚本、按照原有方式配置  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 扩展事件会话，如同早期版本中支持的一样。  
  
 所有 Analysis Services 事件都可以按照 [扩展事件](../../relational-databases/extended-events/extended-events.md)中的定义进行捕获或者针对特定的使用者。  
  
> [!NOTE]  
>  观看此 [快速视频简介](https://www.youtube.com/watch?v=ja2mOHWRVC0&index=1&list=PLv2BtOtLblH1YvzQ5YnjfQFr_oKEvMk19) 或阅读 [支持的博客文章](http://blogs.msdn.com/b/analysisservices/archive/2015/09/22/using-extended-events-with-sql-server-analysis-services-2016-cpt-2-3.aspx) ，了解有关 SQL Server 2016 中 Analysis Services 的 xEvents 详细信息。  
  
  
##  <a name="bkmk_ssas_extended_events_ssms"></a> 使用 Management Studio 配置 Analysis Services  
 对于表格和多维实例，Management Studio 提供了新的管理文件夹，其中包含用户启动的 xEvent 会话。 可以一次运行多个会话。 但在当前实现中， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 扩展事件用户界面不支持更新或重播现有会话。  
  
 ![ssas_extended_events_ssms_start](../../analysis-services/instances/media/ssas-extended-events-ssms-start.png "ssas_extended_events_ssms_start")  
  
 **选择事件**  
  
 如果已经知道想要捕获的事件，搜索它们是将它们添加到跟踪的最简单方法。 否则，通常将使用以下事件用于监视操作：  
  
-   **CommandBegin** 和 **CommandEnd**。  
  
-   **QueryBegin**、 **QueryEnd**和 **QuerySubcubeVerbose** （显示发送至服务器的整个 MDX 或 DAX 查询），以及 **ResourceUsage** （关于查询所用资源和所返回行数的统计信息）。  
  
-   **ProgressReportBegin** 和 **ProgressReportEnd** （用于处理操作）。  
  
-   **AuditLogin** 和 **AuditLogout** （捕获客户端应用程序连接到 Analysis Services 所依据的用户标识）。  
  
 **选择数据存储**  
  
 会话可实时流式传输到 Management Studio 中的窗口，或持久保存到文件供以后使用 Power Query 或 Excel 进行分析。  
  
-   **event_file** 将会话数据存储在 .xel 文件中。  
  
-   **event_stream** 在 Management Studio 中启用“查看实时数据”选项。  
  
-   只要服务器在运行，**ring_buffer** 就会将会话数据存储在内存中。 服务器重新启动后，将给出会话数据  
  
 **添加事件字段**  
  
 请务必配置会话以包含事件字段，以便可以轻松看到感兴趣的信息。  
  
 “配置”是对话框远端的选项。  
  
 ![ssas-xevents-configure](../../analysis-services/instances/media/ssas-xevents-configure.PNG "ssas-xevents-configure")  
  
 在配置中的“事件字段”选项卡上，选择“TextData”，这样此字段出现在事件旁边，显示返回的值，包括正在服务器上执行的查询。  
  
 配置所需事件和数据存储的会话后，可以单击脚本按钮以将配置发送到受支持的目标之一，包括文件、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中的新查询以及剪贴板。  
  
 **刷新会话**  
  
 一旦创建会话，确保刷新 Management Studio 中的会话文件夹，查看刚创建的会话。 如果配置了 event_stream，可以右键单击会话名称，然后选择“查看实时数据”以实时监视服务器活动。  
  
##  <a name="bkmk_script_start"></a> 启动 Analysis Services 中的扩展事件的 XMLA 脚本  
 通过使用如下的 XMLA 创建对象脚本命令启用扩展事件跟踪：  
  
```  
<Execute …>  
   <Command>  
      <Batch …>  
         <Create …>  
            <ObjectDefinition>  
               <Trace>  
                  <ID>trace_id</ID>  
                  <Name>trace_name</Name>  
                  <ddl300_300:XEvent>  
                     <event_session …>  
                        <event package="AS" name="AS_event">  
                           <action package="PACKAGE0" …/>  
                        </event>  
                        <target package="PACKAGE0" name="asynchronous_file_target">  
                           <parameter name="filename" value="data_filename.xel"/>  
                           <parameter name="metadatafile" value="metadata_filename.xem"/>  
                        </target>  
                     </event_session>  
                  </ddl300_300:XEvent>  
               </Trace>  
            </ObjectDefinition>  
         </Create>  
      </Batch>  
   </Command>  
   <Properties></Properties>  
</Execute>  
  
```  
  
 其中，以下元素将由用户根据跟踪需要进行定义：  
  
 *trace_id*  
 定义用于此跟踪的唯一标识符。  
  
 *跟踪名称*  
 提供给此跟踪的名称；通常是此跟踪的用户可读定义。 通常使用 trace_id 值作为该名称。  
  
 *AS_event*  
 要公开的 Analysis Services 事件。 有关事件名称的详细信息，请参阅 [Analysis Services 跟踪事件](https://docs.microsoft.com/bi-reference/trace-events/analysis-services-trace-events) 。  
  
 *data_filename*  
 包含事件数据的文件的名称。 该名称以时间戳作为后缀，以免在反复发送跟踪时数据被覆盖。  
  
 *元数据文件名*  
 包含事件元数据的文件的名称。 该名称以时间戳作为后缀，以免在反复发送跟踪时数据被覆盖。  
  
  
##  <a name="bkmk_script_stop"></a> 停止 Analysis Services 中的扩展事件的 XMLA 脚本  
 若要停止扩展事件跟踪对象，您需要使用如下所示的 XMLA 删除对象脚本命令删除该对象：  
  
```  
<Execute xmlns="urn:schemas-microsoft-com:xml-analysis">  
   <Command>  
      <Batch …>  
         <Delete …>  
            <Object>  
               <TraceID>trace_id</TraceID>  
            </Object>  
         </Delete>  
      </Batch>  
   </Command>  
   <Properties></Properties>  
</Execute>  
  
```  
  
 其中，以下元素将由用户根据跟踪需要进行定义：  
  
 *trace_id*  
 为要删除的跟踪定义唯一标识符。  
  
  
## <a name="see-also"></a>另请参阅  
 [扩展事件](../../relational-databases/extended-events/extended-events.md)  
  
  
