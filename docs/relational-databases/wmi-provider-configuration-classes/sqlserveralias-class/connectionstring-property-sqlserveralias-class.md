---
title: ConnectionString 属性 （SqlServerAlias 类） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: reference
apiname:
- ConnectionString Property (SqlServerAlias Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
helpviewer_keywords:
- ConnectionString property
ms.assetid: 8a3692b9-3a34-42e2-b0b9-28e6bd3a7aba
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 7c2bedb961d8a6063c766ae5f6c31b5895e96c8f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47824326"
---
# <a name="connectionstring-property-sqlserveralias-class"></a>ConnectionString 属性（SqlServerAlias 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  获取用于建立服务器连接别名连接的连接字符串。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.ConnectionString [= value]  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 一个[SqlServerAlias 类](../../../relational-databases/wmi-provider-configuration-classes/sqlserveralias-class/sqlserveralias-class.md)对象，表示[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]别名。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个字符串，指定用于建立服务器连接别名代表的连接的连接字符串。  
  
## <a name="remarks"></a>备注  
  
