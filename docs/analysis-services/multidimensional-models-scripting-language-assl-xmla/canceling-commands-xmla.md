---
title: "取消命令 (XMLA) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- connections [XML for Analysis]
- associated connections [XML for Analysis]
- XML for Analysis, canceling
- associated sessions [XML for Analysis]
- canceling connections
- canceling commands
- canceling sessions
- SPID
- XMLA, canceling
- server process IDs [XML for Analysis]
- sessions [XML for Analysis]
ms.assetid: b59f8197-c33d-4e65-9022-848ccba540f5
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e74ce7bd5b03aa84b6c6580342504148a62a68bf
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="canceling-commands-xmla"></a>取消命令 (XMLA)
  具体取决于发出该命令的用户的管理权限[取消](../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md)命令在 XML 中 Analysis (XMLA) 可以在会话、 会话、 连接、 服务器进程或相关联的会话上取消命令或连接。  
  
## <a name="canceling-commands"></a>取消命令  
 用户可以通过发送取消当前的显式会话的上下文中的当前正在执行命令**取消**命令没有指定属性。  
  
> [!NOTE]  
>  用户不能取消隐式会话中正在运行的命令。  
  
### <a name="canceling-batch-commands"></a>取消 Batch 命令  
 如果用户取消**批处理**命令，则尚未执行内的所有剩余命令**批处理**命令已取消。 如果**批处理**命令事务，任何命令之前执行**取消**命令运行都将回滚。  
  
## <a name="canceling-sessions"></a>取消会话  
 通过指定对于显式会话中的会话标识符[SessionID](../../analysis-services/xmla/xml-elements-properties/sessionid-element-xmla.md)属性**取消**命令时，数据库管理员或服务器管理员可以取消会话，其中包括当前正在执行命令。 数据库管理员只能取消其拥有管理权限的数据库的会话。  
  
 数据库管理员可以通过检索 DISCOVER_SESSIONS 架构行集来检索指定数据库的活动会话。 若要检索 DISCOVER_SESSIONS 架构行集，数据库管理员应使用 XMLA**发现**方法并指定 SESSION_CURRENT_DATABASE 限制列的相应数据库标识符中[限制](../../analysis-services/xmla/xml-elements-properties/restrictions-element-xmla.md)属性**发现**方法。  
  
## <a name="canceling-connections"></a>取消连接  
 通过指定中的连接标识符[ConnectionID](../../analysis-services/xmla/xml-elements-properties/connectionid-element-xmla.md)属性**取消**命令时，服务器管理员可以取消所有与给定的连接，包括所有相关联的会话运行命令，并取消连接。  
  
> [!NOTE]  
>  如果实例[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]找不到并取消与连接关联的会话，例如当数据抽取打开时提供的 HTTP 连接的多个会话，实例无法取消该连接。 如果在执行期间遇到这种情况下，则**取消**命令时，将会出错。  
  
 服务器管理员可以检索的活动连接[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]通过检索使用 XMLA DISCOVER_CONNECTIONS 架构行集的实例**发现**方法。  
  
## <a name="canceling-server-processes"></a>取消服务器进程  
 通过在指定服务器进程标识符 (SPID) [SPID](../../analysis-services/xmla/xml-elements-properties/spid-element-xmla.md)属性**取消**命令时，服务器管理员可以取消与给定 SPID 相关联的命令。  
  
## <a name="canceling-associated-sessions-and-connections"></a>取消关联的会话和连接  
 你可以设置[CancelAssociated](../../analysis-services/xmla/xml-elements-properties/cancelassociated-element-xmla.md)属性为 true 以取消连接、 会话和连接、 会话或中指定的 SPID 与关联的命令**取消**命令。  
  
## <a name="see-also"></a>另请参阅  
 [发现方法 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-methods-discover.md)   
 [使用 Analysis Services 中的 XMLA 进行开发](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  

