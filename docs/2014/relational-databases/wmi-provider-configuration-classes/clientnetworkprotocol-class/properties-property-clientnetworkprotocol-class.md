---
title: Properties 属性 （ClientNetworkProtocol 类） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- Properties Property (ClientNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- Properties property
ms.assetid: 7e0a4e38-4555-4750-8fd3-4425b29e6aa1
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: d6c2dbfb1254260f5c92df5f1da33ba26e368aa7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63192048"
---
# <a name="properties-property-clientnetworkprotocol-class"></a>Properties 属性（ClientNetworkProtocol 类）
  获取与指定的当前客户端网络协议关联的属性[配置客户端协议](https://technet.microsoft.com/library/ms181035.aspx)。  
  
## <a name="syntax"></a>语法  
  
```  
  
object  
.Properties [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *object*  
 一个表示 [客户端使用的网络协议的](clientnetworkprotocol-class.md) ClientNetworkProtocol 类 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个数组[ClientNetworkProtocolProperty 类](../clientnetworkprotocolproperty-class/clientnetworkprotocolproperty-class.md)表示被引用的当前客户端网络协议支持的属性的对象`OrderValue`属性。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [配置客户端网络协议和网络库](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
