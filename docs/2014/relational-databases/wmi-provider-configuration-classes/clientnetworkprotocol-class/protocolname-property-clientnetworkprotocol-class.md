---
title: ProtocolName 属性（ClientNetworkProtocol 类） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- ProtocolName Property (ClientNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- ProtocolName property
ms.assetid: f8527121-fbcd-4d30-9b4a-1461149cb5a8
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 40fdd268536aecd8fc3ce06922d6145188d85a97
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85065612"
---
# <a name="protocolname-property-clientnetworkprotocol-class"></a>ProtocolName 属性（ClientNetworkProtocol 类）
  获取[配置客户端协议](https://technet.microsoft.com/library/ms181035.aspx)指定的当前网络协议的名称。  
  
## <a name="syntax"></a>语法  
  
```  
  
object  
.ProtocolName [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *object*  
 一个表示客户端使用的网络协议的[ClientNetworkProtocol 类](clientnetworkprotocol-class.md)对象 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个字符串值，该值指定[SetOrderValue 方法（ClientNetworkProtocol 类）](https://technet.microsoft.com/library/ms179295.aspx)引用的当前客户端网络协议的名称。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [配置客户端网络协议和网络库](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
