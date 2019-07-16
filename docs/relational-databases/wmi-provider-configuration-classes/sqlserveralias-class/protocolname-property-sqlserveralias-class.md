---
title: ProtocolName 属性 （SqlServerAlias 类） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- ProtocolName Property (SqlServerAlias Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ProtocolName property
ms.assetid: 8fb81ab3-15f1-4a71-be72-2072c6bcc670
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 74c78cd8f90890814921d7b1ce78e65ab8c78a08
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68052427"
---
# <a name="protocolname-property-sqlserveralias-class"></a>ProtocolName 属性（SqlServerAlias 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  获取服务器连接别名使用的协议的名称。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.ProtocolName [= value]  
```  
  
## <a name="parts"></a>部件  
 *object*  
 一个[SqlServerAlias 类](../../../relational-databases/wmi-provider-configuration-classes/sqlserveralias-class/sqlserveralias-class.md)对象，表示[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]别名。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个指定服务器连接别名使用的协议的名称的字符串值。  
  
## <a name="remarks"></a>备注  
  
