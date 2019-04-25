---
title: AliasName 属性 （SqlServerAlias 类） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- AliasName Property (SqlServerAlias Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
helpviewer_keywords:
- AliasName property
ms.assetid: 5c4c88f3-c1cf-471a-9d91-f47657933e2f
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 2cb100265cdb49fba1728900829344e024190db1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62632216"
---
# <a name="aliasname-property-sqlserveralias-class"></a>AliasName 属性（SqlServerAlias 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  获取服务器连接别名的名称。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.AliasName [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *object*  
 一个[SqlServerAlias 类](../../../relational-databases/wmi-provider-configuration-classes/sqlserveralias-class/sqlserveralias-class.md)对象，表示[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]别名。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个**字符串**值，该值指定服务器连接别名的名称。  
  
## <a name="remarks"></a>备注  
  
