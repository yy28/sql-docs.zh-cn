---
title: "NumberOfFlags 属性 （SInstance 类） |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- NumberOfFlags Property (SInstance Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- NumberOfFlags property
ms.assetid: b62005f8-9af3-4fc8-9344-a1ccdb713053
caps.latest.revision: 
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9b2afd1aec33e51ec8130f8c3e97844aaa3902a9
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/19/2018
---
# <a name="numberofflags-property-sinstance-class"></a>NumberOfFlags 属性（SInstance 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  获取的实例数标志[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.NumberOfFlags [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *对象*  
 [SInstance 类](../../../relational-databases/wmi-provider-configuration-classes/sinstance-class/sinstance-class.md)表示的服务器实例的对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 A **uint32**值，该值指定的标志的实例数[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
## <a name="remarks"></a>注释  
  
## <a name="see-also"></a>另请参阅  
 [配置服务器网络协议和网络库](http://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
