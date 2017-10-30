---
title: "脚本组件中的日志记录 |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Script component [Integration Services], logging
ms.assetid: 17c19787-379e-43fe-9107-e36e17ecda53
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 410a2472399574753d67a44b93437b1698c8b086
ms.contentlocale: zh-cn
ms.lasthandoff: 08/03/2017

---
# <a name="logging-in-the-script-component"></a>脚本组件中的日志记录
  使用 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 包中的日志记录可以记录预定义的事件或用户定义的消息，从而将有关执行进度、结果和问题的详细信息保存下来，以供日后分析。 可以使用脚本组件<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A>方法**ScriptMain**类来记录用户定义数据。 如果启用日志记录，和**ScriptComponentLogEntry**来登录选择事件**详细信息**选项卡**配置 SSIS 日志**对话框中，一次对<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A>方法将事件信息存储在已经为数据流任务配置的所有日志提供程序。  
  
 下面是一个简单的日志记录示例：  
  
 `Dim bt(0) As Byte`  
  
 `Me.Log("Test Log Event", _`  
  
 `0, _`  
  
 `bt)`  
  
> [!NOTE]  
>  尽管可以直接从脚本组件执行日志记录，但是您可能希望考虑实现事件，而不是日志记录。 如果使用事件，不仅能够启用事件消息的日志记录，而且能够通过默认的或用户定义的事件处理程序响应事件。  
  
 有关日志记录的详细信息，请参阅[Integration Services &#40;SSIS &#41;日志记录](../../../integration-services/performance/integration-services-ssis-logging.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Integration Services &#40;SSIS &#41;日志记录](../../../integration-services/performance/integration-services-ssis-logging.md)  
  
  

