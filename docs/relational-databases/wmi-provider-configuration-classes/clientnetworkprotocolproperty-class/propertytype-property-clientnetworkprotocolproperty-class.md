---
title: PropertyType 属性 （ClientNetworkProtocolProperty 类） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- PropertyType Property (ClientNetworkProtocolProperty Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- PropertyType property
ms.assetid: fc0e4725-979f-4517-a8f5-25436b87f5c2
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 0239d74c4ff805c484a45a5ac681b00288da6e4d
ms.sourcegitcommit: 6c9d35d03c1c349bc82b9ed0878041d976b703c6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/06/2018
ms.locfileid: "51216395"
---
# <a name="propertytype-property-clientnetworkprotocolproperty-class"></a>PropertyType 属性（ClientNetworkProtocolProperty 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  获取引用属性的类型[PropertyIdx 属性 （ClientNetworkProtocolProperty 类）](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocolproperty-class/propertyidx-property-clientnetworkprotocolproperty-class.md)值。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.PropertyType [= value]  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 一个[ClientNetworkProtocolProperty 类](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocolproperty-class/clientnetworkprotocolproperty-class.md)对象，表示使用的网络协议的属性[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]客户端。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个**uint32**值，该值指定属性的类型。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [配置客户端协议](../../../database-engine/configure-windows/configure-client-protocols.md)  
  
  
