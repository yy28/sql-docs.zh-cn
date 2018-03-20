---
title: "PauseService 方法 （SqlService 类） |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
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
- PauseService Method (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- PauseService method
ms.assetid: 5c3a8feb-58b8-4385-b4c8-bf33cf4d276d
caps.latest.revision: 
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 567941dde0de5f8fb8d3aeeeba5d3c77d24ac6e2
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/19/2018
---
# <a name="pauseservice-method-sqlservice-class"></a>PauseService 方法（SqlService 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  尝试将服务置于暂停状态。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.PauseService()  
```  
  
## <a name="parts"></a>组成部分  
 *对象*  
 一个表示服务的 [SqlService 类](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) 对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个 uint32 值，如果服务已成功停止，则为 0；如果不支持请求，则为 1；其他任何数字表示出现错误。  
  
## <a name="remarks"></a>注释  
  
## <a name="see-also"></a>另请参阅  
 [启动和停止服务](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
