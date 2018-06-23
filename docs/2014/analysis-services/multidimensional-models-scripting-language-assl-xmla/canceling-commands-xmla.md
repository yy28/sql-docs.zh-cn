---
title: 取消命令 (XMLA) |Microsoft 文档
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
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
manager: mblythe
ms.openlocfilehash: 5129dd84cdd120b778fb55986374d27055b5904c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36016954"
---
# <a name="canceling-commands-xmla"></a>取消命令 (XMLA)
  具体取决于发出该命令的用户的管理权限[取消](../xmla/xml-elements-commands/cancel-element-xmla.md)命令在 XML 中 Analysis (XMLA) 可以在会话、 会话、 连接、 服务器进程或相关联的会话上取消命令或连接。  
  
## <a name="canceling-commands"></a>取消命令  
 用户可以通过发送不带任何指定属性的 `Cancel` 命令，取消当前显式会话上下文中当前正在执行的命令。  
  
> [!NOTE]  
>  用户不能取消隐式会话中正在运行的命令。  
  
### <a name="canceling-batch-commands"></a>取消 Batch 命令  
 如果用户取消了一个 `Batch` 命令，则会取消该 `Batch` 命令中尚未执行的所有其余命令。 如果 `Batch` 命令是事务性的，则会回滚在 `Cancel` 命令运行前已执行的所有命令。  
  
## <a name="canceling-sessions"></a>取消会话  
 通过指定对于显式会话中的会话标识符[SessionID](../xmla/xml-elements-properties/id-element-xmla.md)属性`Cancel`命令时，数据库管理员或服务器管理员可以取消会话，包括当前正在执行的命令. 数据库管理员只能取消其拥有管理权限的数据库的会话。  
  
 数据库管理员可以通过检索 DISCOVER_SESSIONS 架构行集来检索指定数据库的活动会话。 若要检索 DISCOVER_SESSIONS 架构行集，数据库管理员应使用 XMLA`Discover`方法并指定 SESSION_CURRENT_DATABASE 限制列中的相应数据库标识符[限制](../xmla/xml-elements-properties/restrictions-element-xmla.md)属性`Discover`方法。  
  
## <a name="canceling-connections"></a>取消连接  
 通过指定中的连接标识符[ConnectionID](../xmla/xml-elements-properties/connectionid-element-xmla.md)属性`Cancel`命令时，服务器管理员可以取消所有与给定的连接，包括所有正在运行的命令，关联的会话和取消连接。  
  
> [!NOTE]  
>  如果实例[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]找不到并取消与连接关联的会话，例如当数据抽取打开时提供的 HTTP 连接的多个会话，实例无法取消该连接。 如果在执行 `Cancel` 命令时遇到了这种情况，则会发生错误。  
  
 服务器管理员可以检索 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的活动连接，方法是使用 XMLA `Discover` 方法检索 DISCOVER_CONNECTIONS 架构行集。  
  
## <a name="canceling-server-processes"></a>取消服务器进程  
 通过在指定服务器进程标识符 (SPID) [SPID](../xmla/xml-elements-properties/spid-element-xmla.md)属性`Cancel`命令时，服务器管理员可以取消与给定 SPID 相关联的命令。  
  
## <a name="canceling-associated-sessions-and-connections"></a>取消关联的会话和连接  
 你可以设置[CancelAssociated](../xmla/xml-elements-properties/cancelassociated-element-xmla.md)属性为 true 以取消连接、 会话和连接、 会话或中指定的 SPID 与关联的命令`Cancel`命令。  
  
## <a name="see-also"></a>请参阅  
 [发现方法&#40;XMLA&#41;](../xmla/xml-elements-methods-discover.md)   
 [在 Analysis Services 中使用 XMLA 开发](developing-with-xmla-in-analysis-services.md)  
  
  