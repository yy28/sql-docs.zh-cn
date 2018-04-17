---
title: AliasName 属性 （SqlServerAlias 类） |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
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
- AliasName Property (SqlServerAlias Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
helpviewer_keywords:
- AliasName property
ms.assetid: 5c4c88f3-c1cf-471a-9d91-f47657933e2f
caps.latest.revision: 31
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9f63001750fae36a68bb172dd9c69e12d1e3f538
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="aliasname-property-sqlserveralias-class"></a>AliasName 属性（SqlServerAlias 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  获取服务器连接别名的名称。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.AliasName [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *对象*  
 A [SqlServerAlias 类](../../../relational-databases/wmi-provider-configuration-classes/sqlserveralias-class/sqlserveralias-class.md)对象，表示[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]别名。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 A**字符串**值，该值指定服务器连接别名的名称。  
  
## <a name="remarks"></a>注释  
  
