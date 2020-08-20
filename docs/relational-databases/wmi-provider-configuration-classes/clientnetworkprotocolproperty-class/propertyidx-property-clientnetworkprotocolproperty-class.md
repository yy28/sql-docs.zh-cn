---
description: PropertyIdx 属性（ClientNetworkProtocolProperty 类）
title: 'PropertyIdx 属性 (ClientNetworkProtocolProperty) '
ms.custom: seo-lt-2019
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
ms.openlocfilehash: 2ca822cf7cde476254410b944258b14415319cb5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88485234"
---
# <a name="propertyidx-property-clientnetworkprotocolproperty-class"></a>PropertyIdx 属性（ClientNetworkProtocolProperty 类）
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  获取或设置属性数组中属性的索引值，该属性由[ClientNetworkProtocol 类](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md)对象[ (ClientNetworkProtocol 类) 属性属性](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/properties-property-clientnetworkprotocol-class.md)引用。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.PropertyIdx [= value]  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 表示客户端使用的网络协议属性的 [ClientNetworkProtocolProperty 类](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocolproperty-class/clientnetworkprotocolproperty-class.md) 对象 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个指定当前属性的数组索引值的 **uint32** 值。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [配置客户端协议](../../../database-engine/configure-windows/configure-client-protocols.md)  
  
  
