---
title: "SetOrderValue 方法 （ClientNetworkProtocol 类） |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: SetOrderValue Method (ClientNetworkProtocol Class)
apilocation: sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords: SetOrderValue method
ms.assetid: 15f693fd-37f6-41d9-9dab-d2c93db19895
caps.latest.revision: "33"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: be269f8784d3812c0110bfbc12c53f1ad6cca7d0
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="setordervalue-method-clientnetworkprotocol-class"></a>SetOrderValue 方法（ClientNetworkProtocol 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]从客户端协议列表中选择具有指定的顺序值的协议。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.SetOrderValue(OrderValue)  
```  
  
## <a name="parts"></a>组成部分  
 *对象*  
 A [ClientNetworkProtocol 类](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md)对象，表示使用的网络协议[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]客户端。  
  
#### <a name="parameters"></a>Parameters  
  
|参数|Description|  
|---------------|-----------------|  
|*OrderValue*|一个设置顺序值的 u**int32** 值。|  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个 **uint32** 值，如果服务已成功修改，则为 0；如果不支持请求，则为 1；其他任何数字表示出现错误。  
  
## <a name="remarks"></a>注释  
  
## <a name="see-also"></a>另请参阅  
 [客户端协议属性（“顺序”选项卡）](http://technet.microsoft.com/library/ms187884.aspx)  
  
  
