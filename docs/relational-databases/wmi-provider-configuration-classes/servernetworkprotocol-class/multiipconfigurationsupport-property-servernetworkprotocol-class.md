---
title: "MultiIpConfigurationSupport 属性 （ServerNetworkProtocol 类） |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- MultiIpConfigurationSupport Property (ServerNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- MultiIpConfigurationSupport property
ms.assetid: 442c6133-4038-42db-a67d-2631285ac76b
caps.latest.revision: 
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ff331a1e296a43bc911fd7fc522b10a663841846
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/19/2018
---
# <a name="multiipconfigurationsupport-property-servernetworkprotocol-class"></a>MultiIpConfigurationSupport 属性（ServerNetworkProtocol 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  获取用于指定服务器网络协议是否支持多个 IP 地址的布尔值属性。  
  
## <a name="syntax"></a>語法  
  
```  
  
object.MultiIpConfigurationSupport [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *对象*  
 A [ProtocolName 属性 （ServerNetworkProtocol 类）](../../../relational-databases/wmi-provider-configuration-classes/servernetworkprotocol-class/protocolname-property-servernetworkprotocol-class.md)对象，表示的实例所使用的网络协议[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个布尔值，指定是否由服务器网络协议支持多个 IP 地址： **true**的服务器网络协议，支持多个 IP 地址或**false**如果通过服务器网络协议不支持多个 IP 地址。  
  
## <a name="remarks"></a>注释  
  
## <a name="see-also"></a>另请参阅  
 [配置服务器网络协议和网络库](http://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
