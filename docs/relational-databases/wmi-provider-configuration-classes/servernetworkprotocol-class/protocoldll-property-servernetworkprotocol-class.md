---
title: "ProtocolDLL 属性 （ServerNetworkProtocol 类） |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: ProtocolDLL Property (ServerNetworkProtocol Class)
apilocation: sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords: ProtocolDLL property
ms.assetid: ac386558-392e-46f3-97f8-382f267b7fca
caps.latest.revision: "31"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 131aec37d58b6dfe18f60d3a45c37fc939e8cca3
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="protocoldll-property-servernetworkprotocol-class"></a>ProtocolDLL 属性（ServerNetworkProtocol 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]获取所需的服务器网络协议的.dll 文件的名称。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.ProtocolDLL [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *对象*  
 A [ServerNetworkProtocol 类](../../../relational-databases/wmi-provider-configuration-classes/servernetworkprotocol-class/servernetworkprotocol-class.md)对象，表示的实例所使用的网络协议[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个指定服务器网络协议所需的协议 .dll 文件的字符串值。  
  
## <a name="remarks"></a>注释  
  
## <a name="see-also"></a>另请参阅  
 [配置服务器网络协议和网络库](http://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
