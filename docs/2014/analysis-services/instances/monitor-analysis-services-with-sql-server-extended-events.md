---
title: 使用 SQL Server 扩展事件 (XEvents) 监视 Analysis Services |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: b57cc2fe-52dc-4fa9-8554-5a866e25c6d7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 546ee0df900f25395314adffde19cea01abb481b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62703236"
---
# <a name="use-sql-server-extended-events-xevents-to-monitor-analysis-services"></a>使用 SQL Server 扩展事件 (XEvents) 监视 Analysis Services
  Analysis Services 提供了通过使用跟踪功能[扩展事件](../../relational-databases/extended-events/extended-events.md)。  
  
 扩展事件是针对服务器系统的高度可伸缩和可配置的事件基础结构。 扩展事件是使用非常少的性能资源的轻型性能监视系统。  
  
 所有 Analysis Services 可以捕获事件和目标中定义特定的使用者[扩展事件](../../relational-databases/extended-events/extended-events.md)，通过 Xevent。  
  
## <a name="initiating-extended-events-in-analysis-services"></a>在 Analysis Services 中启动扩展事件  
 通过使用如下的 XMLA 创建对象脚本命令启用扩展事件跟踪：  
  
```  
<Execute ...>  
   <Command>  
      <Batch ...>  
         <Create ...>  
            <ObjectDefinition>  
               <Trace>  
                  <ID>trace_id</ID>  
                  <Name>trace_name</Name>  
                  <ddl300_300:XEvent>  
                     <event_session ...>  
                        <event package="AS" name="AS_event">  
                           <action package="PACKAGE0" .../>  
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
  
## <a name="stopping-extended-events-in-analysis-services"></a>在 Analysis Services 中停止扩展事件  
 若要停止扩展事件跟踪对象，您需要使用如下所示的 XMLA 删除对象脚本命令删除该对象：  
  
```  
<Execute xmlns="urn:schemas-microsoft-com:xml-analysis">  
   <Command>  
      <Batch ...>  
         <Delete ...>  
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
  
  
