---
title: PropertyValType 属性 （ClientNetworkProtocolProperty 类） |Microsoft 文档
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
- PropertyValType Property (ClientNetworkProtocolProperty Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- PropertyValType property
ms.assetid: 624b9bdd-ed93-4140-bd4e-00d714a2558c
caps.latest.revision: 31
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: fd4238a43c5bc8a31e33bae9993c52b05e9e750b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36017038"
---
# <a name="propertyvaltype-property-clientnetworkprotocolproperty-class"></a>PropertyValType 属性（ClientNetworkProtocolProperty 类）
  获取所引用的属性中存储的值的数据类型[PropertyIdx 属性 （ClientNetworkProtocolProperty 类）](clientnetworkprotocolproperty-class.md)值。  
  
## <a name="syntax"></a>语法  
  
```  
  
object  
.PropertyValType [= value]  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 A [ClientNetworkProtocolProperty 类](clientnetworkprotocolproperty-class.md)表示使用的网络协议的属性的对象[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]客户端。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个指定属性值的数据类型的 `uint32` 值。  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>请参阅  
 [配置客户端协议](../../../database-engine/configure-windows/configure-client-protocols.md)  
  
  