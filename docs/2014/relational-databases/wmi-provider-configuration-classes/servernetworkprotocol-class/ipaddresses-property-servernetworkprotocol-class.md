---
title: IpAddresses 属性（ServerNetworkProtocol 类） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- IpAddresses Property (ServerNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- IpAddresses property
ms.assetid: e5d66f7e-9719-436e-b723-12d56f914a05
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: e7b2adf53bc6ebca14e2d3b4dc2cee248a4b6720
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63190303"
---
# <a name="ipaddresses-property-servernetworkprotocol-class"></a>IpAddresses 属性（ServerNetworkProtocol 类）
  获取与服务器网络协议关联的 IP 地址。  
  
## <a name="syntax"></a>语法  
  
```  
  
object  
.IpAddresses [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *对象*  
 一个`ServerNetworkProtocol`对象，该对象表示实例[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]使用的网络协议。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个[ServerNetworkProtocolIPAdress 类](../servernetworkprotocolipaddress-class/servernetworkprotocolipaddress-class.md)对象的数组，这些对象表示服务器网络协议支持的 IP 地址。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [配置服务器网络协议和网络库](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
