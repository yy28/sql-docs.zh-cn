---
title: MultiIpConfigurationSupport 属性 （ServerNetworkProtocol 类） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: reference
apiname:
- MultiIpConfigurationSupport Property (ServerNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- MultiIpConfigurationSupport property
ms.assetid: 442c6133-4038-42db-a67d-2631285ac76b
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 1d13d41d48e9a36bae4bc9ffcab7b84ad6d1f605
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47720975"
---
# <a name="multiipconfigurationsupport-property-servernetworkprotocol-class"></a>MultiIpConfigurationSupport 属性（ServerNetworkProtocol 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  获取用于指定服务器网络协议是否支持多个 IP 地址的布尔值属性。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.MultiIpConfigurationSupport [= value]  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 一个[ProtocolName 属性 （ServerNetworkProtocol 类）](../../../relational-databases/wmi-provider-configuration-classes/servernetworkprotocol-class/protocolname-property-servernetworkprotocol-class.md)对象，表示使用的实例的网络协议[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个布尔值，指定服务器网络协议是否支持多个 IP 地址： **，则返回 true**的服务器网络协议，支持多个 IP 地址或**false**如果服务器网络协议不支持多个 IP 地址。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [配置服务器网络协议和网络库](http://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
