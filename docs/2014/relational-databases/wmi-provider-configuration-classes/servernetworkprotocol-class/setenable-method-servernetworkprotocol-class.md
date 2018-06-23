---
title: SetEnable 方法 （ServerNetworkProtocol 类） |Microsoft 文档
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
- SetEnable Method (ServerNetworkProtocol Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetEnable method
ms.assetid: a287950b-086f-4b6d-a2d8-4d3973bd1b21
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 3b6a51b4432252ffaed1dd2cbc2c269551e8caf5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36016777"
---
# <a name="setenable-method-servernetworkprotocol-class"></a>SetEnable 方法（ServerNetworkProtocol 类）
  启用服务器网络协议。  
  
## <a name="syntax"></a>语法  
  
```  
  
object  
.SetEnable()  
  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 A [ServerNetworkProtocol 类](servernetworkprotocol-class.md)对象，表示的实例所使用的网络协议[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个 `uint32` 值，如果服务已成功修改，则为 0；如果不支持请求，则为 1；其他任何数字表示出现错误。  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>请参阅  
 [配置服务器网络协议和网络库](http://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  