---
title: "SetDisable 方法 （ClientNetworkProtocol 类） |Microsoft 文档"
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
apiname: SetDisable Method (ClientNetworkProtocol Class)
apilocation: sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords: SetDisable method
ms.assetid: bce69ab9-ea5b-43fd-8114-08b1b5890755
caps.latest.revision: "36"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f7d8adb0c74a3fd1ae8de4fb3805e62c58a92887
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="setdisable-method-clientnetworkprotocol-class"></a>SetDisable 方法（ClientNetworkProtocol 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]禁用指定的客户端网络协议[Configure Client Protocols](http://technet.microsoft.com/library/ms181035.aspx)。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.SetDisable()  
```  
  
## <a name="parts"></a>组成部分  
 *对象*  
 A [ClientNetworkProtocol 类](../../../relational-databases/wmi-provider-configuration-classes/clientnetworkprotocol-class/clientnetworkprotocol-class.md)对象，表示使用的网络协议[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]客户端。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个 **uint32** 值，如果服务已成功修改，则为 0；如果不支持请求，则为 1；其他任何数字表示出现错误。  
  
## <a name="remarks"></a>注释  
  
## <a name="see-also"></a>另请参阅  
 [配置客户端网络协议和网络库](http://technet.microsoft.com/library/ms181035.aspx)  
  
  
