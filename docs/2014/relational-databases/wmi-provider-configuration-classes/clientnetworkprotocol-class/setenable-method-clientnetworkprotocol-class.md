---
title: SetEnable 方法 （ClientNetworkProtocol 类） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- SetEnable Method (ClientNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetEnable method
ms.assetid: a66c756a-1311-4f4a-8088-818f8ed90056
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 1aa192f2dc78a424b1d4c8792044caac0934173a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62826717"
---
# <a name="setenable-method-clientnetworkprotocol-class"></a>SetEnable 方法（ClientNetworkProtocol 类）
  启用指定的客户端网络协议[配置客户端协议](https://technet.microsoft.com/library/ms181035.aspx)。  
  
## <a name="syntax"></a>语法  
  
```  
  
object  
.SetEnableMethod()  
  
```  
  
## <a name="parts"></a>组成部分  
 *object*  
 一个[ClientNetworkProtocol 类](clientnetworkprotocol-class.md)对象，表示使用的网络协议[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]客户端。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个 `uint32` 值，如果服务已成功修改，则为 0；如果不支持请求，则为 1；其他任何数字表示出现错误。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [配置客户端网络协议和网络库](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
