---
title: SupportAlias 属性 （ClientNetworkProtocol 类） |Microsoft 文档
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
- SupportAlias Property (ClientNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SupportAlias property
ms.assetid: 1e7a2e87-c356-40a6-a6d9-e492467629f9
caps.latest.revision: 16
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: be78007f210519c9b9fb67a9e2a67f3697b4a2b8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36128502"
---
# <a name="supportalias-property-clientnetworkprotocol-class"></a>SupportAlias 属性（ClientNetworkProtocol Class）
  获取用于指定是否当前的网络协议指定的布尔属性[SetOrderValue 方法 （ClientNetworkProtocol 类）](clientnetworkprotocol-class.md)支持别名。  
  
## <a name="syntax"></a>语法  
  
```  
  
object  
.SupportAlias [= value]  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 A [ClientNetworkProtocol 类](clientnetworkprotocol-class.md)对象，表示使用的网络协议[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]客户端。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个指定客户端网络协议是否支持别名的布尔值。  
  
 如果为 True，则客户端网络协议支持别名。  
  
 如果为 False，则客户端网络协议不支持别名。  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>请参阅  
 [配置客户端协议](http://technet.microsoft.com/library/ms181035.aspx)  
  
  