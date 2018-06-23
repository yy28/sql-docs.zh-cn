---
title: 取消元素 (XMLA) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Cancel Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.cancel
- http://schemas.microsoft.com/analysisservices/2003/engine#Cancel
- urn:schemas-microsoft-com:xml-analysis#Cancel
helpviewer_keywords:
- Cancel command
ms.assetid: de4062c1-7434-44dc-9f01-29fcf78963bd
caps.latest.revision: 15
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: cd0fdd50a1dcddb51d167ab76cd5408b631bb3ef
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36126623"
---
# <a name="cancel-element-xmla"></a>Cancel 元素 (XMLA)
  取消当前正在运行的命令[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Command>  
   <Cancel>  
      <ConnectionID>...</ConnectionID>  
      <SessionID>...</SessionID>  
      <SPID>...</SPID>  
      <CancelAssociated>...</CancelAssociated>  
   </Cancel>  
</Command>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|InclusionThresholdSetting|  
|默认值|InclusionThresholdSetting|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Command](../xml-elements-properties/command-element-xmla.md)|  
|子元素|[CancelAssociated](../xml-elements-properties/cancelassociated-element-xmla.md)， [ConnectionID](../xml-elements-properties/id-element-xmla.md)， [SessionID](../xml-elements-properties/sessionid-element-xmla.md)， [SPID](../xml-elements-properties/spid-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 `Cancel` 命令取消会话上下文中当前正在执行的命令。 如果客户端应用程序未请求会话，则不能取消命令。  
  
 如果 `Cancel` 命令是在执行 `Batch` 命令期间执行的，则取消整个 `Batch` 命令。 如果 `Batch` 命令是事务性的，则回滚 `Batch` 命令包含的所有命令。 如果 `Batch` 命令不是事务性的，则只回滚在执行 `Batch` 命令时正在执行的 `Cancel` 命令所包含的那些命令。 已执行的非事务性 `Batch` 命令中的命令不会回滚。  
  
 通常，`Cancel` 命令用于取消正在当前活动会话上执行的命令。 在这种情况下，不必为 `Cancel` 命令指定子元素。 管理员还可以使用 `Cancel` 命令取消在当前活动会话之外的其他连接或会话上执行的命令。 具有给定数据库的管理员权限的角色成员可以取消应用于该数据库的连接和会话的命令，而服务器管理员则可以取消给定 Analysis Services 实例的连接和会话的命令。  
  
 若要检索有关 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 实例的当前连接和会话的信息，可以执行 `Discover` 方法以分别请求 DISCOVER_CONNECTIONS 和 DISCOVER_SESSIONS 架构行集。 具有给定数据库的管理员权限的角色成员可以在 DISCOVER_SESSIONS 架构行集的 SESSION_CURRENT_DATABASE 限制列中指定该数据库，以此限定只返回该给定数据库的会话。 有关详细信息`Discover`方法，请参阅[发现方法&#40;XMLA&#41;](../xml-elements-methods-discover.md)。  
  
## <a name="see-also"></a>请参阅  
 [批处理元素&#40;XMLA&#41;](batch-element-xmla.md)   
 [命令&#40;XMLA&#41;](xml-elements-commands.md)  
  
  