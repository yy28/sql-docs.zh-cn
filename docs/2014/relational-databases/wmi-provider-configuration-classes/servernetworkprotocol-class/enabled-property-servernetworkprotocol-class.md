---
title: 启用属性 （ServerNetworkProtocol 类） |Microsoft 文档
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
- Enabled Property (ServerNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- Enabled property
ms.assetid: a514822a-91f1-4aca-9175-2b96cff29700
caps.latest.revision: 32
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 538215095bb15aa34d95ecab70eec6894055ead0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36127252"
---
# <a name="enabled-property-servernetworkprotocol-class"></a>Enabled 属性（ServerNetworkProtocol 类）
  获取指定是否启用服务器网络协议的布尔值。  
  
## <a name="syntax"></a>语法  
  
```  
  
object  
.Enabled [= value]  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 A [ServerNetworkProtocol 类](servernetworkprotocol-class.md)对象，表示的实例所使用的网络协议[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个指定是否启用服务器网络协议的布尔值：如果启用服务器网络协议，则为 `true`；如果禁用服务器网络协议，则为 `false`。  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>请参阅  
 [配置服务器网络协议和网络库](http://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  