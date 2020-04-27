---
title: ProtocolOrder 属性（ClientNetworkProtocol 类） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- ProtocolOrder Property (ClientNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- ProtocolOrder property
ms.assetid: aa09b8ab-37db-4406-8973-acf503855fd2
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 0a0043e5a894e3f3f1b778a6f42fe6e3bacbbc78
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63192886"
---
# <a name="protocolorder-property-clientnetworkprotocol-class"></a>ProtocolOrder 属性（ClientNetworkProtocol 类）
  获取[SetOrderValue 方法（ClientNetworkProtocol 类）](clientnetworkprotocol-class.md)方法指定的当前引用的客户端网络协议的序号。  
  
## <a name="syntax"></a>语法  
  
```  
  
object  
.ProtocolOrder [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *object*  
 一个表示[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]客户端使用的网络协议的[ClientNetworkProtocol 类](clientnetworkprotocol-class.md)对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个 `uint32` 值，用于指定按照 `OrderValue` 方法设置的当前所引用的客户端网络协议的序号。 如果客户端网络协议为禁用状态，则此值将为零。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [配置客户端协议](https://technet.microsoft.com/library/ms181035.aspx)   
 [配置客户端网络协议和网络库](https://technet.microsoft.com/library/ms181035.aspx)  
  
  
