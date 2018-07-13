---
title: DisplayName 属性 （SqlService 类） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- DisplayName Property (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- DisplayName property
ms.assetid: 49c408aa-6eb4-45cd-8d5c-60f065f24f5c
caps.latest.revision: 35
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 2295409a459c9b5264876cc4201beb86cae9a356
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37177324"
---
# <a name="displayname-property-sqlservice-class"></a>DisplayName 属性（SqlService 类）
  获取服务的显示名称。  
  
## <a name="syntax"></a>语法  
  
```  
  
object  
.DisplayName [= value]  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 一个表示服务的 [SqlService 类](sqlservice-class.md) 对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个指定服务的显示名称的字符串值。  
  
## <a name="remarks"></a>Remarks  
 此字符串的最大长度为 256 个字符。 此名称在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 配置管理器中是区分大小写的。 但是，显示名称比较始终不区分大小写。  
  
## <a name="example"></a>示例  
  
```  
mysqlservice.DisplayName = "Atdisk"  
```  
  
## <a name="see-also"></a>请参阅  
 [启动和停止服务](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
