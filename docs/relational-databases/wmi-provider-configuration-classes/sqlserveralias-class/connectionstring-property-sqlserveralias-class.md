---
description: ConnectionString 属性（SqlServerAlias 类）
title: 'ConnectionString 属性 (SqlServerAlias) '
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- ConnectionString Property (SqlServerAlias Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
helpviewer_keywords:
- ConnectionString property
ms.assetid: 8a3692b9-3a34-42e2-b0b9-28e6bd3a7aba
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0b0a8cacce04ad0ef376d7ed6516b017f3c1b85d
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/08/2020
ms.locfileid: "89550903"
---
# <a name="connectionstring-property-sqlserveralias-class"></a>ConnectionString 属性（SqlServerAlias 类）
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  获取用于建立服务器连接别名连接的连接字符串。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.ConnectionString [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *object*  
 一个表示别名的 [SqlServerAlias 类](../../../relational-databases/wmi-provider-configuration-classes/sqlserveralias-class/sqlserveralias-class.md) 对象 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个字符串，指定用于建立服务器连接别名代表的连接的连接字符串。  
  
## <a name="remarks"></a>备注  
  
