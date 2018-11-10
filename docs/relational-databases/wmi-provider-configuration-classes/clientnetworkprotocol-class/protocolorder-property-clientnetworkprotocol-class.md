---
title: ProtocolOrder 属性 （ClientNetworkProtocol 类） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- ProtocolOrder Property (ClientNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ProtocolOrder property
ms.assetid: aa09b8ab-37db-4406-8973-acf503855fd2
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 48a57927e050d04370f903b35c78866241430a55
ms.sourcegitcommit: 6c9d35d03c1c349bc82b9ed0878041d976b703c6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/06/2018
ms.locfileid: "51217375"
---
# <a name="protocolorder-property-clientnetworkprotocol-class"></a>ProtocolOrder 属性（ClientNetworkProtocol 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  获取由指定的网络协议的当前引用的客户端的订单号[SetOrderValue 方法 （ClientNetworkProtocol 类）](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/setordervalue-method-clientnetworkprotocol-class.md)方法。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.ProtocolOrder [= value]  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 一个[ClientNetworkProtocol 类](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md)对象，表示使用的网络协议[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]客户端。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个**uint32**值，该值指定所设置的当前引用的客户端网络协议的订单号**OrderValue**方法。 如果客户端网络协议为禁用状态，则此值将为零。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [配置客户端协议](http://technet.microsoft.com/library/ms181035.aspx)   
 [配置客户端网络协议和网络库](http://technet.microsoft.com/library/ms181035.aspx)  
  
  
