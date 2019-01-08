---
title: IpAddresses 属性 （ServerNetworkProtocol 类） |Microsoft Docs
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
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/13/2018
ms.locfileid: "53371329"
---
# <a name="ipaddresses-property-servernetworkprotocol-class"></a>IpAddresses 属性（ServerNetworkProtocol 类）
  获取与服务器网络协议关联的 IP 地址。  
  
## <a name="syntax"></a>语法  
  
```  
  
object  
.IpAddresses [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *object*  
 一个`ServerNetworkProtocol`对象，表示使用的实例的网络协议[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个数组[ServerNetworkProtocolIPAdress 类](../servernetworkprotocolipaddress-class/servernetworkprotocolipaddress-class.md)对象表示服务器网络协议支持的 IP 地址。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [配置服务器网络协议和网络库](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
