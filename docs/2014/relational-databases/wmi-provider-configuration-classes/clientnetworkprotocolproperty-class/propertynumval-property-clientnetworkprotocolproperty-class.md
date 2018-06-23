---
title: PropertyNumVal 属性 （ClientNetworkProtocolProperty 类） |Microsoft 文档
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
- PropertyNumVal Property (ClientNetworkProtocolProperty Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- PropertyNumVal property
ms.assetid: 12b02d97-702b-434f-baf6-e49a6b2cd4de
caps.latest.revision: 28
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 0e737aaa1d5b224e096a7ae6f3f70b81884ba9f1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36017039"
---
# <a name="propertynumval-property-clientnetworkprotocolproperty-class"></a>PropertyNumVal 属性（ClientNetworkProtocolProperty 类）
  获取所引用的当前属性的数值[PropertyIdx 属性 （ClientNetworkProtocolProperty 类）](clientnetworkprotocolproperty-class.md)值。  
  
## <a name="syntax"></a>语法  
  
```  
  
object  
.PropertyNumVal [= value]  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 A [ClientNetworkProtocolProperty 类](clientnetworkprotocolproperty-class.md)表示使用的网络协议的属性的对象[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]客户端。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个指定当前属性的数值的 u`int32` 值。  
  
## <a name="remarks"></a>Remarks  
  