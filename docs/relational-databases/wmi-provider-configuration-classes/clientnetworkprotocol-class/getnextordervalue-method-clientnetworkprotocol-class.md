---
title: "GetNextOrderValue 方法 （ClientNetworkProtocol 类） |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- GetNextOrderValue Method (ClientNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- GetNextOrderValue method
ms.assetid: d741dc5c-c225-43d9-a730-7ad664ac525f
caps.latest.revision: 
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 92f93aa53145c87b0841519b8910f8d67c05080a
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/19/2018
---
# <a name="getnextordervalue-method-clientnetworkprotocol-class"></a>GetNextOrderValue 方法（ClientNetworkProtocol 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  选择位于协议列表中的下一个位置的协议。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.GetNextOrderValue()  
```  
  
## <a name="parts"></a>组成部分  
 *对象*  
 A [ClientNetworkProtocol 类](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md)对象，表示使用的网络协议[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]客户端。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个 **uint32** 值，如果服务已成功修改，则为 0；如果不支持请求，则为 1；其他任何数字表示出现错误。  
  
## <a name="remarks"></a>注释  
  
## <a name="see-also"></a>另请参阅  
 [配置客户端协议](http://technet.microsoft.com/library/ms181035.aspx)   
 [配置客户端网络协议和网络库](http://technet.microsoft.com/library/ms181035.aspx)  
  
  
