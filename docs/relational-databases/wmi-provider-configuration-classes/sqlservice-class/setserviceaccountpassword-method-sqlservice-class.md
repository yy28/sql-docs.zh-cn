---
title: SetServiceAccountPassword 方法 （SqlService 类） |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: reference
apiname:
- SetServiceAccountPassword Method (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetServiceAccountPassword method
ms.assetid: e577a1ac-985c-4799-bb38-9393efc3def2
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 4c09b309ed20c5362843f7cafac37dbd6dbc9c71
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47838545"
---
# <a name="setserviceaccountpassword-method-sqlservice-class"></a>SetServiceAccountPassword 方法（SqlService 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  修改引用的服务运行时使用的帐户的密码。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.SetServiceAccountPassword(AccountOldPassword , ServiceStartPassword)  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 一个表示服务的 [SqlService 类](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) 对象。  
  
#### <a name="parameters"></a>Parameters  
 *AccountOldPassword*  
 一个指定帐户的现有密码的字符串值。  
  
 *ServiceStartPassword*  
 一个指定帐户的新密码的字符串值。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个 **uint32** 值，如果服务已成功修改，则为 0；如果不支持请求，则为 1；其他任何数字表示出现错误。  
  
## <a name="remarks"></a>备注  
  
