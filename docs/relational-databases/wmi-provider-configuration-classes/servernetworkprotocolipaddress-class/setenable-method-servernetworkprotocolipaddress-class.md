---
description: SetEnable 方法（ServerNetworkProtocolIPAddress 类）
title: 'SetEnable 方法 (ServerNetworkProtocolIPAddress) '
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetEnable Method (ServerNetworkProtocolIPAddress Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetEnable method
ms.assetid: baa86deb-95dd-416f-b2c7-cec1dfb91ab4
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 52f19e66fcb11941dadfcaf9e1bb85e8001b0b1f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88446140"
---
# <a name="setenable-method-servernetworkprotocolipaddress-class"></a>SetEnable 方法（ServerNetworkProtocolIPAddress 类）
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  启用 IP 地址。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.SetEnable()  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 一个表示实例上的网络协议 IP 地址的 [ServerNetworkProtocolIPAdress 类](../../../relational-databases/wmi-provider-configuration-classes/servernetworkprotocolipaddress-class/servernetworkprotocolipaddress-class.md) 对象 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个 **uint32** 值，如果服务已成功修改，则为 0；如果不支持请求，则为 1；其他任何数字表示出现错误。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [配置服务器网络协议和网络库](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
