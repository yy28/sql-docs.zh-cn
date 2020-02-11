---
title: SetStringValue 方法（ClientNetworkProtocolProperty 类） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- SetStringValue Method (ClientNetworkProtocolProperty Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetStringValue method
ms.assetid: 88d67b22-0eea-48c9-ab73-e0b4907953df
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 82b89246d6289d0b19ee97e68e94f77d7cb30a77
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63244987"
---
# <a name="setstringvalue-method-clientnetworkprotocolproperty-class"></a>SetStringValue 方法（ClientNetworkProtocolProperty 类）
  设置[PropertyIdx 属性（ClientNetworkProtocolProperty 类）](clientnetworkprotocolproperty-class.md)值引用的当前属性的字符串值。  
  
## <a name="syntax"></a>语法  
  
```  
  
object  
.SetStringValue(  
StrValue  
)  
  
```  
  
## <a name="parts"></a>组成部分  
 *对象*  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)]表示[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]客户端使用的网络协议属性的[ClientNetworkProtocolProperty 类](clientnetworkprotocolproperty-class.md)对象。  
  
#### <a name="parameters"></a>parameters  
  
|参数|说明|  
|---------------|-----------------|  
|*StrValue*|一个指定当前属性的新值的字符串值。|  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个 `uint32` 值，如果服务已成功修改，则为 0；如果不支持请求，则为 1；其他任何数字表示出现错误。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [配置客户端协议](../../../database-engine/configure-windows/configure-client-protocols.md)  
  
  
