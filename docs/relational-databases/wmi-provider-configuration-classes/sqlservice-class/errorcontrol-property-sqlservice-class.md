---
title: "ErrorControl 属性 （SqlService 类） |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
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
- ErrorControl Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ErrorControl property
ms.assetid: cbb1e0fa-5bfc-4b1b-a6ed-f7d5cfad4d73
caps.latest.revision: 
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b04e7e57d9a9c66766aa744807e36bc05a96a8b0
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/19/2018
---
# <a name="errorcontrol-property-sqlservice-class"></a>ErrorControl 属性（SqlService 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  获取或设置启动期间服务无法启动时的错误严重性。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.ErrorControl [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *对象*  
 一个表示服务的 [SqlService 类](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) 对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个字符串值，用于指定启动期间服务无法启动时所报告的错误的严重性。 下表列出了可能的值。  
  
 Ignore  
 不通知用户。  
  
 正常  
 通知用户。  
  
 Severe  
 使用上一次已知正确的配置重新启动系统。  
  
 严重  
 系统将尝试使用正确的配置重新启动。  
  
 Unknown  
 严重性未知。  
  
## <a name="remarks"></a>注释  
 此值指示出现故障时启动程序采取的操作。 所有的错误都由计算机系统记录。  
  
## <a name="see-also"></a>另请参阅  
 [启动和停止服务](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
