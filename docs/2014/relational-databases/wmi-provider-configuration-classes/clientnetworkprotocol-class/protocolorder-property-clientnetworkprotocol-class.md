---
title: ProtocolOrder 属性 （ClientNetworkProtocol 类） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- ProtocolOrder Property (ClientNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- ProtocolOrder property
ms.assetid: aa09b8ab-37db-4406-8973-acf503855fd2
caps.latest.revision: 34
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 26d3e5d3251d3954ba8c8410b48d471070bcba50
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37266203"
---
# <a name="protocolorder-property-clientnetworkprotocol-class"></a>ProtocolOrder 属性（ClientNetworkProtocol 类）
  获取由指定的网络协议的当前引用的客户端的订单号[SetOrderValue 方法 （ClientNetworkProtocol 类）](clientnetworkprotocol-class.md)方法。  
  
## <a name="syntax"></a>语法  
  
```  
  
object  
.ProtocolOrder [= value]  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 一个[ClientNetworkProtocol 类](clientnetworkprotocol-class.md)对象，表示使用的网络协议[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]客户端。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个 `uint32` 值，用于指定按照 `OrderValue` 方法设置的当前所引用的客户端网络协议的序号。 如果客户端网络协议为禁用状态，则此值将为零。  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>请参阅  
 [配置客户端协议](http://technet.microsoft.com/library/ms181035.aspx)   
 [配置客户端网络协议和网络库](http://technet.microsoft.com/library/ms181035.aspx)  
  
  
