---
title: 使用 SQL Server 扩展事件 (XEvents) 监视 Analysis Services |Microsoft 文档
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b57cc2fe-52dc-4fa9-8554-5a866e25c6d7
caps.latest.revision: 5
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: eb67c1eca2b803c01a3716708f73afbb3861476a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36126955"
---
# <a name="use-sql-server-extended-events-xevents-to-monitor-analysis-services"></a>使用 SQL Server 扩展事件 (XEvents) 监视 Analysis Services
  Analysis Services 跟踪通过提供功能的使用情况[扩展事件](../../relational-databases/extended-events/extended-events.md)。  
  
 扩展事件是针对服务器系统的高度可伸缩和可配置的事件基础结构。 扩展事件是使用非常少的性能资源的轻型性能监视系统。  
  
 所有 Analysis Services 事件可以捕获和对特定的使用者，如中定义的目标[扩展事件](../../relational-databases/extended-events/extended-events.md)，通过 Xevent。  
  
## <a name="initiating-extended-events-in-analysis-services"></a>在 Analysis Services 中启动扩展事件  
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
 要公开的 Analysis Services 事件。 有关事件名称的详细信息，请参阅 [Analysis Services 跟踪事件](../trace-events/analysis-services-trace-events.md) 。  
  
 *data_filename*  
 包含事件数据的文件的名称。 该名称以时间戳作为后缀，以免在反复发送跟踪时数据被覆盖。  
  
 *元数据文件名*  
 包含事件元数据的文件的名称。 该名称以时间戳作为后缀，以免在反复发送跟踪时数据被覆盖。  
  
## <a name="stopping-extended-events-in-analysis-services"></a>在 Analysis Services 中停止扩展事件  
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
  
## <a name="see-also"></a>请参阅  
 [扩展事件](../../relational-databases/extended-events/extended-events.md)  
  
  