---
description: Enabled 属性（ServerNetworkProtocolIpAddress 类）
title: '已启用属性 (ServerNetworkProtocolIpAddress) '
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- Enabled Property (ServerNetworkProtocolIpAddress Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- Enabled property
ms.assetid: 870fd4d0-6c77-462a-b480-d42eb044b2e7
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6d339c0bbd465c20c56762d75d1e42553027478f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/08/2020
ms.locfileid: "89539997"
---
# <a name="enabled-property-servernetworkprotocolipaddress-class"></a>Enabled 属性（ServerNetworkProtocolIpAddress 类）
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  获取指定是否启用 IP 地址的布尔值。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.Enabled [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *object*  
 一个表示实例上的网络协议 IP 地址的 [ServerNetworkProtocolIPAdress 类](../../../relational-databases/wmi-provider-configuration-classes/servernetworkprotocolipaddress-class/servernetworkprotocolipaddress-class.md) 对象 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 指定是否启用 IP 地址的布尔值：如果启用了 ip 地址， **则为 true** ; 如果禁用了 ip 地址，则为 **false** 。  
  
## <a name="see-also"></a>另请参阅  
 [配置服务器网络协议和网络库](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
