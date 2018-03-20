---
title: "ConnectionString 属性 （SqlServerAlias 类） |Microsoft 文档"
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
- ConnectionString Property (SqlServerAlias Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
helpviewer_keywords:
- ConnectionString property
ms.assetid: 8a3692b9-3a34-42e2-b0b9-28e6bd3a7aba
caps.latest.revision: 
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: db3cfeef1b61e84ca7e99b557e9e2236cd21bc3d
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/19/2018
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
  
