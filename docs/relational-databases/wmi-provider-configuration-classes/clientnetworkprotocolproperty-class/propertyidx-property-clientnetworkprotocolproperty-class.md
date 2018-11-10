---
title: PropertyIdx 属性 （ClientNetworkProtocolProperty 类） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- PropertyIdx Property (ClientNetworkProtocolProperty Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- PropertyIdx property
ms.assetid: d7845962-ac68-4435-9c59-70ec450fec88
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: b8a088c5a02f010bda32da9b67b962e5445c02ab
ms.sourcegitcommit: 6c9d35d03c1c349bc82b9ed0878041d976b703c6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/06/2018
ms.locfileid: "51214718"
---
# <a name="propertyidx-property-clientnetworkprotocolproperty-class"></a>PropertyIdx 属性（ClientNetworkProtocolProperty 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  获取或设置该属性的索引值中引用的属性数组[Properties 属性 （ClientNetworkProtocol 类）](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/properties-property-clientnetworkprotocol-class.md)的[ClientNetworkProtocol 类](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md)对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.PropertyIdx [= value]  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 一个[ClientNetworkProtocolProperty 类](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocolproperty-class/clientnetworkprotocolproperty-class.md)对象，表示使用的网络协议的属性[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]客户端。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个**uint32**值，该值指定当前属性的数组索引值。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [配置客户端协议](../../../database-engine/configure-windows/configure-client-protocols.md)  
  
  
