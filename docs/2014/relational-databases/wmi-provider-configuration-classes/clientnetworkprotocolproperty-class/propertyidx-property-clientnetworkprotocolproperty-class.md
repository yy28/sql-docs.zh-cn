---
title: PropertyIdx 属性（ClientNetworkProtocolProperty 类） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- PropertyIdx Property (ClientNetworkProtocolProperty Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- PropertyIdx property
ms.assetid: d7845962-ac68-4435-9c59-70ec450fec88
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 08a46d5f73c485306be2f6d0b5086f715ebb00d1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63245109"
---
# <a name="propertyidx-property-clientnetworkprotocolproperty-class"></a>PropertyIdx 属性（ClientNetworkProtocolProperty 类）
  获取或设置由[ClientNetworkProtocol 类](../clientnetworkprotocol-class/clientnetworkprotocol-class.md)对象的[Properties 属性（ClientNetworkProtocol 类）](../clientnetworkprotocol-class/clientnetworkprotocol-class.md)引用的属性数组中的属性的索引值。  
  
## <a name="syntax"></a>语法  
  
```  
  
object  
.PropertyIdx [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *对象*  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)]表示[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]客户端使用的网络协议属性的[ClientNetworkProtocolProperty 类](clientnetworkprotocolproperty-class.md)对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个指定当前属性的数组索引值的 `uint32` 值。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [配置客户端协议](../../../database-engine/configure-windows/configure-client-protocols.md)  
  
  
