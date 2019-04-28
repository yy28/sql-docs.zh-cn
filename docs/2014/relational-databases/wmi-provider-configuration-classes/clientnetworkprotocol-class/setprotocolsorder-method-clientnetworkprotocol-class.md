---
title: SetProtocolsOrder 方法 （ClientNetworkProtocol 类） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- SetProtocolsOrder Method (ClientNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetProtocolsOrder method
ms.assetid: b86d98b9-aae4-4e74-b4da-1ec984d5c8b4
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 16a939835d5129a12d5c3b9fce9d6fa5e0c07f80
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62826605"
---
# <a name="setprotocolsorder-method-clientnetworkprotocol-class"></a>SetProtocolsOrder 方法（ClientNetworkProtocol 类）
  更改协议列表的顺序。  
  
## <a name="syntax"></a>语法  
  
```  
  
object  
.SetProtocolsOrder(  
ProtocolOrderList  
)  
  
```  
  
## <a name="parts"></a>组成部分  
 *object*  
 一个[ClientNetworkProtocol 类](clientnetworkprotocol-class.md)对象，表示使用的网络协议[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]客户端。  
  
#### <a name="parameters"></a>Parameters  
  
|参数|Description|  
|---------------|-----------------|  
|*ProtocolOrderList*|一个以新的顺序列出客户端网络协议的字符串数组。|  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个 `uint32` 值，如果服务已成功修改，则为 0；如果不支持请求，则为 1；其他任何数字表示出现错误。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [配置客户端协议](https://technet.microsoft.com/library/ms181035.aspx)   
 [配置客户端网络协议和网络库](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
