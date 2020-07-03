---
title: MultiIpConfigurationSupport 属性（ServerNetworkProtocol）
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- MultiIpConfigurationSupport Property (ServerNetworkProtocol
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- MultiIpConfigurationSupport property
ms.assetid: 442c6133-4038-42db-a67d-2631285ac76b
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0ff19a1a89c301b018a9231ca8c98277d6a55e43
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85888732"
---
# <a name="multiipconfigurationsupport-property-servernetworkprotocol-class"></a>MultiIpConfigurationSupport 属性（ServerNetworkProtocol 类）
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  获取用于指定服务器网络协议是否支持多个 IP 地址的布尔值属性。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.MultiIpConfigurationSupport [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *object*  
 表示实例使用的网络协议的[ProtocolName 属性（ServerNetworkProtocol 类）](../../../relational-databases/wmi-provider-configuration-classes/servernetworkprotocol-class/protocolname-property-servernetworkprotocol-class.md)对象 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 指定服务器网络协议是否支持多个 IP 地址的布尔值：如果服务器网络协议支持多个 ip 地址，**则为 true** ; 如果服务器网络协议不支持多个 ip 地址，则为**false** 。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [配置服务器网络协议和网络库](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
