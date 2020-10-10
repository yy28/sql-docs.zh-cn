---
description: Properties 属性（ClientNetworkProtocol 类）
title: 'Properties 属性 (ClientNetworkProtocol) '
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- Properties Property (ClientNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- Properties property
ms.assetid: 7e0a4e38-4555-4750-8fd3-4425b29e6aa1
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ba9dfe13c38f4f29dd06c313c16896f34857a746
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/09/2020
ms.locfileid: "91890197"
---
# <a name="properties-property-clientnetworkprotocol-class"></a>Properties 属性（ClientNetworkProtocol 类）
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  获取与 [配置客户端协议](../../../database-engine/configure-windows/configure-client-protocols.md)指定的当前客户端网络协议关联的属性。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.Properties [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *object*  
 一个表示 [客户端使用的网络协议的](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) ClientNetworkProtocol 类 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个 [ClientNetworkProtocolProperty 类](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocolproperty-class/clientnetworkprotocolproperty-class.md) 对象的数组，这些对象表示由 **OrderValue** 属性引用的当前客户端网络协议支持的属性。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [配置客户端网络协议和网络库](../../../database-engine/configure-windows/configure-client-protocols.md)  
  
