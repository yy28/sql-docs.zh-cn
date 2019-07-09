---
title: 断开用户连接和会话上 Analysis Services 服务器 |Microsoft Docs
ms.date: 07/05/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 696c6548dadda2412566acf7fae1e2cff2b28095
ms.sourcegitcommit: 9af07bd57b76a34d3447e9e15f8bd3b17709140a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/08/2019
ms.locfileid: "67624401"
---
# <a name="disconnect-users-and-sessions-on-analysis-services-server"></a>断开 Analysis Services 服务器上用户和会话的连接
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]
  作为管理员，你可能需要结束用户活动作为工作负荷管理的一部分。 可以通过取消会话和连接来完成这一任务。 会话可以在运行查询时隐式自动形成，也可以在创建会话时由管理员显式命名。 连接是开放的管道，可以通过连接运行查询。 会话和连接均可在处于活动状态时结束。 例如，可能要结束处理时间太长，是否产生了怀疑正在执行的命令被正确写入并处理会话。  
  
## <a name="ending-sessions-and-connections"></a>结束会话和连接  
 若要管理会话和连接，请使用动态管理视图 (Dmv) 和 XMLA:  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中，连接到 Analysis Services 实例。  
  
2.  将以下任一个 DMV 查询粘贴到 MDX 查询窗口中，以获取当前正在执行的所有会话、连接和命令的列表：  
  
     `Select * from $System.Discover_Sessions`  
  
     `Select * from $System.Discover_Connections`  （此查询不适用于 Azure Analysis Services）
  
     `Select * from $System.Discover_Commands`  
  
3.  按 F5 执行该查询。  
  
     DMV 查询以易于读取和复制的表格结果集返回会话和连接信息。  
  
 保持查询窗口处于打开状态。 在下一步骤中，你将希望返回至本页以复制你要断开连接的会话的 SPID。  
  
 若要结束会话，请打开另一个 XMLA 查询窗口。  
  
1.  将以下语法粘贴到 MDX 查询窗口中，用从上一步中复制的有效值替换 ConnectionID、SessionID 或 SPID 占位符。  
  
    ```  
    <Cancel xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
  
       <ConnectionID>111</ConnectionID>  
       <SessionID>222</SessionID>  
       <SPID>333</SPID>  
  
    <CancelAssociated>1</CancelAssociated>  
    </Cancel>  
  
    ```  
  
2.  按 F5 执行取消命令。  

正在取消 SPID/SessionID 将取消与 SPID/SessionID 相对应的会话上运行任何活动命令。 正在取消连接将确定与连接关联的会话，并取消该会话上运行任何活动命令。 在极少数情况下，不会关闭连接如果引擎无法跟踪所有会话和 Spid 相关联的连接;例如，当多个会话在打开的 HTTP 方案中。   
  
若要了解有关本主题中引用的 XMLA 的详细信息，请参阅[执行的方法&#40;XMLA&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute)并[取消元素&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/cancel-element-xmla)。  
  
## <a name="see-also"></a>请参阅  
 [管理连接和会话 (XMLA)](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/managing-connections-and-sessions-xmla.md)   
 [BeginSession 元素 (XMLA)](https://docs.microsoft.com/bi-reference/xmla/xml-elements-headers/beginsession-element-xmla)   
 [EndSession 元素 (XMLA)](https://docs.microsoft.com/bi-reference/xmla/xml-elements-headers/endsession-element-xmla)   
 [Session 元素 (XMLA)](https://docs.microsoft.com/bi-reference/xmla/xml-elements-headers/session-element-xmla)  
  
  
