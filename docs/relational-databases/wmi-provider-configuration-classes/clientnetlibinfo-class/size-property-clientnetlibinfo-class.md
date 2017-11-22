---
title: "Size 属性 （ClientNetLibInfo 类） |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Size Property (ClientNetLibInfo Class)
apilocation: sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords: Size property
ms.assetid: 66f7264e-2c18-40f5-8091-b5dd83d5716f
caps.latest.revision: "30"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1842de4cb9be91aee1e6b331959c8e4ac626b434
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="size-property-clientnetlibinfo-class"></a>Size 属性（ClientNetLibInfo 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]获取客户端的大小中千字节为单位的网络库。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.Size [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *对象*  
 一个表示有关客户端网络库的信息的 [ClientNetLibInfo 类](../../../relational-databases/wmi-provider-configuration-classes/clientnetlibinfo-class/clientnetlibinfo-class.md) 对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个指定客户端网络库文件的大小的 uint32 值 (KB)。  
  
## <a name="remarks"></a>注释  
  
## <a name="see-also"></a>另请参阅  
 [配置客户端协议](http://technet.microsoft.com/library/ms181035.aspx)  
  
  
