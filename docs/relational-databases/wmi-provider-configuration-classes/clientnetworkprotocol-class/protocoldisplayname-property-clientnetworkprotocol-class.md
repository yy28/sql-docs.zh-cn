---
description: ProtocolDisplayName 属性（ClientNetworkProtocol 类）
title: 'ProtocolDisplayName 属性 (ClientNetworkProtocol) '
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- ProtocolDisplayName Property (ClientNetworkProtocol Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ProtocolDisplayName property
ms.assetid: af194304-5600-48b5-9e93-c2fa95594909
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e0779c737456a9b898895cab2b187fa090b0a6fc
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/09/2020
ms.locfileid: "91888925"
---
# <a name="protocoldisplayname-property-clientnetworkprotocol-class"></a>ProtocolDisplayName 属性（ClientNetworkProtocol 类）
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  获取 [配置客户端协议](../../../database-engine/configure-windows/configure-client-protocols.md)指定的客户端网络协议的显示名称。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.ProtocolDisplayName [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *object*  
 一个表示客户端使用的网络协议的 [ClientNetworkProtocol 类](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md) 对象 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个指定客户端网络协议的显示名称的字符串值。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [配置客户端网络协议和网络库](../../../database-engine/configure-windows/configure-client-protocols.md)  
  
