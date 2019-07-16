---
title: SetStrValue 方法 （ClientNetworkProtocolProperty 类） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetStrValue Method (ClientNetworkProtocolProperty Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetStrValue method
ms.assetid: 4ff80124-6e2e-4d96-a692-57c17b53c55e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5edd424f06b53ef1a530a47b390640a7a1d8b604
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68072552"
---
# <a name="setstrvalue-method-clientnetworkprotocolproperty-class"></a>SetStrValue 方法（ClientNetworkProtocolProperty 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  设置引用的当前属性的字符串值[PropertyIdx 属性 （ClientNetworkProtocolProperty 类）](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocolproperty-class/propertyidx-property-clientnetworkprotocolproperty-class.md)值。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.SetStrValue(StrValue)  
```  
  
## <a name="parts"></a>部件  
 *object*  
 一个[ClientNetworkProtocolProperty 类](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocolproperty-class/clientnetworkprotocolproperty-class.md)对象，表示使用的网络协议的属性[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]客户端。  
  
#### <a name="parameters"></a>Parameters  
  
|参数|描述|  
|---------------|-----------------|  
|*StrValue*|一个指定当前属性的新值的字符串值。|  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个 uint32 值，如果服务已成功修改，则为 0；如果不支持请求，则为 1；其他任何数字表示出现错误。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [配置客户端协议](../../../database-engine/configure-windows/configure-client-protocols.md)  
  
  
