---
title: PropertyValType 属性 （ServerNetworkProtocolProperty 类） |Microsoft 文档
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
- PropertyValType Property (ServerNetworkProtocolProperty Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- PropertyValType property
ms.assetid: fbd42e8e-0642-4a19-b3c8-6ce88345145f
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: ca660a1c991e11a15a6968eb539c36cbb63c223b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36018131"
---
# <a name="propertyvaltype-property-servernetworkprotocolproperty-class"></a>PropertyValType 属性（ServerNetworkProtocolProperty 类）
  获取存储在所引用属性中的值的数据类型。  
  
## <a name="syntax"></a>语法  
  
```  
  
object  
.PropertyValType [= value]  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 A [ServerNetworkProtocolProperty 类](servernetworkprotocolproperty-class.md)表示的实例上的网络协议的属性的对象[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个指定属性值的数据类型的 `uint32` 值。 如果是字符串值类型，则返回 0；如果是数值类型，则返回 1。  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>请参阅  
 [配置服务器网络协议和网络库](http://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  