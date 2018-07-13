---
title: Properties 属性 （ServerNetworkProtocol 类） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Properties Property (ServerNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- Properties property
ms.assetid: 6c971bfc-c277-4c1e-a06e-146dcc34e759
caps.latest.revision: 29
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: cf3384908284cb25a59c35451706b0e3e535e345
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37157868"
---
# <a name="properties-property-servernetworkprotocol-class"></a>Properties 属性（ServerNetworkProtocol 类）
  获取与服务器网络协议关联的属性。  
  
## <a name="syntax"></a>语法  
  
```  
  
object  
.Properties [= value]  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 一个[ServerNetworkProtocol 类](servernetworkprotocol-class.md)对象，表示使用的实例的网络协议[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个数组[ServerNetworkProtocolProperty 类](../servernetworkprotocolproperty-class/servernetworkprotocolproperty-class.md)表示服务器网络协议支持的属性的对象。  
  
## <a name="remarks"></a>Remarks  
  
