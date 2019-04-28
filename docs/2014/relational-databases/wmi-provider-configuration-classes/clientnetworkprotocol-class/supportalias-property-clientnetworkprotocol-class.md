---
title: SupportAlias 属性 （ClientNetworkProtocol 类） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
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
ms.openlocfilehash: d28ec166f8954b874f98b7f9f441280ab9064f1f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62826753"
---
# <a name="supportalias-property-clientnetworkprotocol-class"></a>SupportAlias 属性（ClientNetworkProtocol Class）
  获取指定当前网络是否指定协议的布尔属性[SetOrderValue 方法 （ClientNetworkProtocol 类）](clientnetworkprotocol-class.md)支持别名。  
  
## <a name="syntax"></a>语法  
  
```  
  
object  
.SupportAlias [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *object*  
 一个表示 [客户端使用的网络协议的](clientnetworkprotocol-class.md) ClientNetworkProtocol 类 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个指定客户端网络协议是否支持别名的布尔值。  
  
 如果为 True，则客户端网络协议支持别名。  
  
 如果为 False，则客户端网络协议不支持别名。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [配置客户端协议](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
