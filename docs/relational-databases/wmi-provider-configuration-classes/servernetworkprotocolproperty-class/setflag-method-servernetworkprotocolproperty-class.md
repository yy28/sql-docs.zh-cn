---
description: SetFlag 方法（ServerNetworkProtocolProperty 类）
title: 'SetFlag 方法 (ServerNetworkProtocolProperty) '
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetFlag Method (ServerNetworkProtocolProperty Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetFlag method
ms.assetid: 95288931-8eb1-4477-ad80-619cf7073e61
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 726835f48299c1184b103029cdd0ef419435e987
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88485167"
---
# <a name="setflag-method-servernetworkprotocolproperty-class"></a>SetFlag 方法（ServerNetworkProtocolProperty 类）
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  设置引用的属性的标志。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.SetFlag(BoolValue)  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 一个表示实例上的网络协议属性的 [ServerNetworkProtocolProperty 类](../../../relational-databases/wmi-provider-configuration-classes/servernetworkprotocolproperty-class/servernetworkprotocolproperty-class.md) 对象 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
#### <a name="parameters"></a>参数  
  
|参数|描述|  
|---------------|-----------------|  
|*BoolValue*|一个指定标志的新值的布尔值。|  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个 **uint32** 值，如果服务已成功修改，则为 0；如果不支持请求，则为 1；其他任何数字表示出现错误。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [配置服务器网络协议和网络库](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
