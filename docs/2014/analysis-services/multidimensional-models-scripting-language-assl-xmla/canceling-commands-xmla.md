---
title: 取消命令（XMLA） |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
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
author: minewiskan
ms.author: owend
ms.openlocfilehash: 003c70362c38ae1838b4679abf6485fa031a9143
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84545059"
---
# <a name="canceling-commands-xmla"></a>取消命令 (XMLA)
  根据发出命令的用户的管理权限，XML for Analysis （XMLA）中的[cancel](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/cancel-element-xmla)命令可取消会话、会话、连接、服务器进程或关联会话或连接的命令。  
  
## <a name="canceling-commands"></a>取消命令  
 用户可以通过发送不带任何指定属性的 `Cancel` 命令，取消当前显式会话上下文中当前正在执行的命令。  
  
> [!NOTE]  
>  用户不能取消隐式会话中正在运行的命令。  
  
### <a name="canceling-batch-commands"></a>取消 Batch 命令  
 如果用户取消了一个 `Batch` 命令，则会取消该 `Batch` 命令中尚未执行的所有其余命令。 如果 `Batch` 命令是事务性的，则会回滚在 `Cancel` 命令运行前已执行的所有命令。  
  
## <a name="canceling-sessions"></a>取消会话  
 通过在命令的[SessionID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/id-element-xmla)属性中指定显式会话的会话标识符 `Cancel` ，数据库管理员或服务器管理员可以取消会话，包括当前正在执行的命令。 数据库管理员只能取消其拥有管理权限的数据库的会话。  
  
 数据库管理员可以通过检索 DISCOVER_SESSIONS 架构行集来检索指定数据库的活动会话。 为了检索 DISCOVER_SESSIONS 架构行集，数据库管理员使用 XMLA `Discover` 方法，并为该方法的[限制](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/restrictions-element-xmla)属性中的 "SESSION_CURRENT_DATABASE 限制" 列指定相应的数据库标识符 `Discover` 。  
  
## <a name="canceling-connections"></a>取消连接  
 通过在命令的[ConnectionID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/connectionid-element-xmla)属性中指定连接标识符 `Cancel` ，服务器管理员可以取消与给定连接关联的所有会话，包括所有正在运行的命令，并取消连接。  
  
> [!NOTE]  
>  如果实例 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 无法找到和取消与连接关联的会话（例如，当数据抽取在提供 HTTP 连接的同时打开多个会话时），则实例将无法取消该连接。 如果在执行 `Cancel` 命令时遇到了这种情况，则会发生错误。  
  
 服务器管理员可以检索 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的活动连接，方法是使用 XMLA `Discover` 方法检索 DISCOVER_CONNECTIONS 架构行集。  
  
## <a name="canceling-server-processes"></a>取消服务器进程  
 通过在命令的[SPID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/id-element-xmla)属性中指定服务器进程标识符（SPID） `Cancel` ，服务器管理员可以取消与给定 SPID 关联的命令。  
  
## <a name="canceling-associated-sessions-and-connections"></a>取消关联的会话和连接  
 可以将[CancelAssociated](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cancelassociated-element-xmla)属性设置为 true，以便取消与命令中指定的连接、会话或 SPID 关联的连接、会话和命令 `Cancel` 。  
  
## <a name="see-also"></a>另请参阅  
 [XMLA&#41;&#40;发现方法](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover)   
 [在 Analysis Services 中使用 XMLA 开发](developing-with-xmla-in-analysis-services.md)  
  
  
