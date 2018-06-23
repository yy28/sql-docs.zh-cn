---
title: Properties 属性 （ServerNetworkProtocol 类） |Microsoft 文档
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
- Properties Property (ServerNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- Properties property
ms.assetid: 6c971bfc-c277-4c1e-a06e-146dcc34e759
caps.latest.revision: 29
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 62dc2149afae84eab6fa236d5601c50c9b99c1cd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36137937"
---
# <a name="properties-property-servernetworkprotocol-class"></a>Properties 属性（ServerNetworkProtocol 类）
  获取与服务器网络协议关联的属性。  
  
## <a name="syntax"></a>语法  
  
```  
  
object  
.Properties [= value]  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 A [ServerNetworkProtocol 类](servernetworkprotocol-class.md)对象，表示的实例所使用的网络协议[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 数组[ServerNetworkProtocolProperty 类](../servernetworkprotocolproperty-class/servernetworkprotocolproperty-class.md)表示所支持的服务器网络协议属性的对象。  
  
## <a name="remarks"></a>Remarks  
  