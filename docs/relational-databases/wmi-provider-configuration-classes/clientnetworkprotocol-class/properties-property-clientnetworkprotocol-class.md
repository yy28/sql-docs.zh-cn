---
title: Properties 属性 （ClientNetworkProtocol 类） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- Properties Property (ClientNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- Properties property
ms.assetid: 7e0a4e38-4555-4750-8fd3-4425b29e6aa1
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 6497305d0a0d9a303df0f46e74914b3467243cdf
ms.sourcegitcommit: 6c9d35d03c1c349bc82b9ed0878041d976b703c6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/06/2018
ms.locfileid: "51217685"
---
# <a name="properties-property-clientnetworkprotocol-class"></a>Properties 属性（ClientNetworkProtocol 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  获取与指定的当前客户端网络协议关联的属性[配置客户端协议](http://technet.microsoft.com/library/ms181035.aspx)。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.Properties [= value]  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 一个表示 [客户端使用的网络协议的](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) ClientNetworkProtocol 类 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个数组[ClientNetworkProtocolProperty 类](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocolproperty-class/clientnetworkprotocolproperty-class.md)对象表示通过引用的当前客户端网络协议支持的属性**OrderValue**属性。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [配置客户端网络协议和网络库](http://technet.microsoft.com/library/ms181035.aspx)  
  
  
