---
title: SetOrderValue 方法 （ClientNetworkProtocol 类） |Microsoft 文档
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
- SetOrderValue Method (ClientNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetOrderValue method
ms.assetid: 15f693fd-37f6-41d9-9dab-d2c93db19895
caps.latest.revision: 33
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: ff50a3388fd83c23d13bc201c9c27ffc7f43fd44
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36028526"
---
# <a name="setordervalue-method-clientnetworkprotocol-class"></a>SetOrderValue 方法（ClientNetworkProtocol 类）
  从客户端协议列表中选择具有指定顺序值的协议。  
  
## <a name="syntax"></a>语法  
  
```  
  
object  
.SetOrderValue(  
OrderValue  
)  
  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 A [ClientNetworkProtocol 类](clientnetworkprotocol-class.md)对象，表示使用的网络协议[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]客户端。  
  
#### <a name="parameters"></a>Parameters  
  
|参数|Description|  
|---------------|-----------------|  
|*OrderValue*|一个设置顺序值的 u`int32` 值。|  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个 `uint32` 值，如果服务已成功修改，则为 0；如果不支持请求，则为 1；其他任何数字表示出现错误。  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>请参阅  
 [客户端协议属性（“顺序”选项卡）](http://technet.microsoft.com/library/ms187884.aspx)  
  
  