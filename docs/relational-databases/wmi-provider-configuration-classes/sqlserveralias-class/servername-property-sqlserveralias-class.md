---
description: ServerName 属性（SqlServerAlias 类）
title: 'ServerName 属性 (SqlServerAlias) '
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- ServerName Property (SqlServerAlias Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ServerName property
ms.assetid: 58c82b19-b548-42fa-9c5a-059b606da097
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5bcecf3a22661418aba02b939a824973b30a070d
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/08/2020
ms.locfileid: "89550883"
---
# <a name="servername-property-sqlserveralias-class"></a>ServerName 属性（SqlServerAlias 类）
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  获取 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 服务器连接别名指定的实例的名称。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.ServerName [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *object*  
 一个表示别名的 [SqlServerAlias 类](../../../relational-databases/wmi-provider-configuration-classes/sqlserveralias-class/sqlserveralias-class.md) 对象 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个指定服务器连接别名引用的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的名称的字符串值。  
  
## <a name="remarks"></a>备注  
  
