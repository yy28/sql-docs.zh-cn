---
title: Size 属性 （ClientNetLibInfo 类） |Microsoft 文档
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: wmi
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- Size Property (ClientNetLibInfo Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- Size property
ms.assetid: 66f7264e-2c18-40f5-8091-b5dd83d5716f
caps.latest.revision: 30
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ceb09221a28cdff8c9f72c901ab76d6a7721a0c5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="size-property-clientnetlibinfo-class"></a>Size 属性（ClientNetLibInfo 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  获取客户端网络库文件的大小 (KB)。  
  
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
  
  
