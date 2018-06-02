---
title: 取消元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7bc3cd9330261d0ec4e13a715612d73e6ecb44eb
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/02/2018
ms.locfileid: "34574869"
---
# <a name="cancel-element-xmla"></a>Cancel 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  取消当前正在运行命令的 Analysis Services 实例。  
  
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
|父元素|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|子元素|[CancelAssociated](../../../analysis-services/xmla/xml-elements-properties/cancelassociated-element-xmla.md)， [ConnectionID](../../../analysis-services/xmla/xml-elements-properties/connectionid-element-xmla.md)， [SessionID](../../../analysis-services/xmla/xml-elements-properties/sessionid-element-xmla.md)， [SPID](../../../analysis-services/xmla/xml-elements-properties/spid-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 **取消**命令取消当前正在执行的会话的上下文中的命令。 如果客户端应用程序未请求会话，则不能取消命令。  
  
 如果**取消**的执行过程中执行命令**批处理**命令时，整个**批处理**取消命令。 如果**批处理**命令是事务性的所有包含的命令**批处理**命令都将回滚。 如果**批处理**命令不是事务性的仅包含那些命令**批处理**次执行的命令**取消**执行命令是回滚。 中非事务性命令**批处理**已执行的命令将不会回滚。  
  
 通常情况下，**取消**命令用于在当前处于活动状态的会话上取消正在执行的命令。 在此情况下，无的子元素**取消**必须指定命令。 **取消**命令还可由管理员来取消连接或当前处于活动状态的会话之外的会话上执行的命令。 具有给定数据库的管理员权限的角色成员可以取消应用于该数据库的连接和会话的命令，而服务器管理员则可以取消给定 Analysis Services 实例的连接和会话的命令。  
  
 若要检索有关当前连接和会话信息[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例，**发现**可以执行方法若要请求，分别 DISCOVER_CONNECTIONS 和 DISCOVER_SESSIONS 架构行集。 具有给定数据库的管理员权限的角色成员可以在 DISCOVER_SESSIONS 架构行集的 SESSION_CURRENT_DATABASE 限制列中指定该数据库，以此限定只返回该给定数据库的会话。 有关详细信息**发现**方法，请参阅[发现方法&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-methods-discover.md)。  
  
## <a name="see-also"></a>另请参阅
 [批处理元素&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)   
 [命令&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
