---
title: SupportAlias 属性 （ClientNetworkProtocol 类） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
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
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 2bfb677ba05bc5303c706d65dd2dda70eb67d23d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48082567"
---
# <a name="supportalias-property-clientnetworkprotocol-class"></a>SupportAlias 属性（ClientNetworkProtocol Class）
  获取指定当前网络是否指定协议的布尔属性[SetOrderValue 方法 （ClientNetworkProtocol 类）](clientnetworkprotocol-class.md)支持别名。  
  
## <a name="syntax"></a>语法  
  
```  
  
object  
.SupportAlias [= value]  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 一个[ClientNetworkProtocol 类](clientnetworkprotocol-class.md)对象，表示使用的网络协议[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]客户端。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个指定客户端网络协议是否支持别名的布尔值。  
  
 如果为 True，则客户端网络协议支持别名。  
  
 如果为 False，则客户端网络协议不支持别名。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [配置客户端协议](http://technet.microsoft.com/library/ms181035.aspx)  
  
  
