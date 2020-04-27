---
title: SetStrValue 方法（ClientNetworkProtocolProperty 类） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- SetStrValue Method (ClientNetworkProtocolProperty Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetStrValue method
ms.assetid: 4ff80124-6e2e-4d96-a692-57c17b53c55e
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: fe58a49e707bdca231b488ae207d14bbbfc7cb0a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63242537"
---
# <a name="setstrvalue-method-clientnetworkprotocolproperty-class"></a>SetStrValue 方法（ClientNetworkProtocolProperty 类）
  设置[PropertyIdx 属性（ClientNetworkProtocolProperty 类）](clientnetworkprotocolproperty-class.md)值引用的当前属性的字符串值。  
  
## <a name="syntax"></a>语法  
  
```  
  
object  
.SetStrValue(  
StrValue  
)  
  
```  
  
## <a name="parts"></a>组成部分  
 *object*  
 表示[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]客户端使用的网络协议属性的[ClientNetworkProtocolProperty 类](clientnetworkprotocolproperty-class.md)对象。  
  
#### <a name="parameters"></a>参数  
  
|参数|说明|  
|---------------|-----------------|  
|*StrValue*|一个指定当前属性的新值的字符串值。|  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个 uint32 值，如果服务已成功修改，则为 0；如果不支持请求，则为 1；其他任何数字表示出现错误。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [配置客户端协议](../../../database-engine/configure-windows/configure-client-protocols.md)  
  
  
