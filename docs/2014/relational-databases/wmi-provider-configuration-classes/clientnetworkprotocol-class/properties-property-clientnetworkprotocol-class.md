---
title: Properties 属性 （ClientNetworkProtocol 类） |Microsoft 文档
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
- Properties Property (ClientNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- Properties property
ms.assetid: 7e0a4e38-4555-4750-8fd3-4425b29e6aa1
caps.latest.revision: 33
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 4882f26e1f74fd68e67f14172482bcc674d1b06e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36018130"
---
# <a name="properties-property-clientnetworkprotocol-class"></a>Properties 属性（ClientNetworkProtocol 类）
  获取与指定的当前客户端网络协议关联的属性[Configure Client Protocols](http://technet.microsoft.com/library/ms181035.aspx)。  
  
## <a name="syntax"></a>语法  
  
```  
  
object  
.Properties [= value]  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 A [ClientNetworkProtocol 类](clientnetworkprotocol-class.md)对象，表示使用的网络协议[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]客户端。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 数组[ClientNetworkProtocolProperty 类](../clientnetworkprotocolproperty-class/clientnetworkprotocolproperty-class.md)表示引用的当前客户端网络协议支持的属性的对象`OrderValue`属性。  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>请参阅  
 [配置客户端网络协议和网络库](http://technet.microsoft.com/library/ms181035.aspx)  
  
  