---
title: ConnectionString 属性 （SqlServerAlias 类） |Microsoft 文档
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
- ConnectionString Property (SqlServerAlias Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
helpviewer_keywords:
- ConnectionString property
ms.assetid: 8a3692b9-3a34-42e2-b0b9-28e6bd3a7aba
caps.latest.revision: 30
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 95950cbd1f5c68bf2f192dc096a823805d0985e1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="connectionstring-property-sqlserveralias-class"></a>ConnectionString 属性（SqlServerAlias 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  获取用于建立服务器连接别名连接的连接字符串。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.ConnectionString [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *对象*  
 A [SqlServerAlias 类](../../../relational-databases/wmi-provider-configuration-classes/sqlserveralias-class/sqlserveralias-class.md)对象，表示[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]别名。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个字符串，指定用于建立服务器连接别名代表的连接的连接字符串。  
  
## <a name="remarks"></a>注释  
  
