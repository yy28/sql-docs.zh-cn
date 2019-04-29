---
title: 取消命令 (XMLA) |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 313708ad1575c7b9922ac796791d0d623c51b54b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63182937"
---
# <a name="canceling-commands-xmla"></a>取消命令 (XMLA)
  具体取决于发出该命令的用户的管理权限[取消](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/cancel-element-xmla)Analysis (XMLA) 可以在一个会话、 会话、 连接、 服务器进程或相关联的会话上取消命令的 XML 中的命令或连接。  
  
## <a name="canceling-commands"></a>取消命令  
 用户可以通过发送取消当前显式会话的上下文中当前正在执行命令**取消**命令和任何指定属性。  
  
> [!NOTE]  
>  用户不能取消隐式会话中正在运行的命令。  
  
### <a name="canceling-batch-commands"></a>取消 Batch 命令  
 如果用户取消**批处理**命令，则所有剩余的命令中尚未执行**批处理**命令已取消。 如果**批处理**命令是事务性的前, 已执行的所有命令**取消**命令运行都将回滚。  
  
## <a name="canceling-sessions"></a>取消会话  
 对于显式会话中指定的会话标识符[SessionID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/id-element-xmla)的属性**取消**命令时，数据库管理员或服务器管理员可以取消会话，其中包括当前正在执行命令。 数据库管理员只能取消其拥有管理权限的数据库的会话。  
  
 数据库管理员可以通过检索 DISCOVER_SESSIONS 架构行集来检索指定数据库的活动会话。 若要检索 DISCOVER_SESSIONS 架构行集，数据库管理员需要使用 XMLA**发现**方法，并指定相应的数据库标识符为 SESSION_CURRENT_DATABASE 限制列中[限制](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/restrictions-element-xmla)属性**Discover**方法。  
  
## <a name="canceling-connections"></a>取消连接  
 通过指定中的连接标识符[ConnectionID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/connectionid-element-xmla)的属性**取消**命令时，服务器管理员可以取消所有与给定的连接，包括所有关联的会话运行命令，并取消该连接。  
  
> [!NOTE]
>  如果实例[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]无法找到和取消与连接关联的会话，如该实例时数据抽取打开了多个会话提供 HTTP 连接时，不能取消该连接。 如果在执行期间遇到这种情况下**取消**命令时，出现错误。  
  
 服务器管理员可以检索的活动连接数[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]实例通过检索 DISCOVER_CONNECTIONS 架构行集使用 XMLA**发现**方法。  
  
## <a name="canceling-server-processes"></a>取消服务器进程  
 通过指定服务器进程标识符 (SPID) 中[SPID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/id-element-xmla)的属性**取消**命令时，服务器管理员可以取消与给定 SPID 关联的命令。  
  
## <a name="canceling-associated-sessions-and-connections"></a>取消关联的会话和连接  
 可以设置[CancelAssociated](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cancelassociated-element-xmla)属性设为 true 来取消连接、 会话和连接、 会话或 SPID 中指定与关联的命令**取消**命令。  
  
## <a name="see-also"></a>请参阅  
 [发现方法&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover)   
 [在 Analysis Services 中使用 XMLA 开发](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
