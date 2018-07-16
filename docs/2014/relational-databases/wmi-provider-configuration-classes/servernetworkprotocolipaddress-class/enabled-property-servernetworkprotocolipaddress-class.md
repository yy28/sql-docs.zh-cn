---
title: 启用属性 （ServerNetworkProtocolIpAddress 类） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Enabled Property (ServerNetworkProtocolIpAddress Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- Enabled property
ms.assetid: 870fd4d0-6c77-462a-b480-d42eb044b2e7
caps.latest.revision: 14
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: a2296ec80dc8c97fef8588b810d5d4179dd5ed7c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37268503"
---
# <a name="enabled-property-servernetworkprotocolipaddress-class"></a>Enabled 属性（ServerNetworkProtocolIpAddress 类）
  获取指定是否启用 IP 地址的布尔值。  
  
## <a name="syntax"></a>语法  
  
```  
  
object  
.Enabled [= value]  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 一个[ServerNetworkProtocolIPAdress 类](servernetworkprotocolipaddress-class.md)对象，表示的实例上的网络协议 IP 地址[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个指定是否启用 IP 地址的布尔值：如果启用 IP 地址，则为 `true`；如果禁用 IP 地址，则为 `false`。  
  
## <a name="see-also"></a>请参阅  
 [配置服务器网络协议和网络库](http://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
