---
title: DisplayName 属性 （SqlService 类） |Microsoft 文档
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
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 3a6cb6dcbc9872f049e3c534296a26b1028b991b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36013837"
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
  
  