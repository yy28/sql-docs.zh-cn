---
title: "DisplayName 属性 （SqlService 类） |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: DisplayName Property (SqlService Class)
apilocation: sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords: DisplayName property
ms.assetid: 49c408aa-6eb4-45cd-8d5c-60f065f24f5c
caps.latest.revision: "35"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 20c247d8581099dc797c2ea05fc2eab91dfcb51a
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="displayname-property-sqlservice-class"></a>DisplayName 属性（SqlService 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]获取服务的显示名称。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.DisplayName [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *对象*  
 一个表示服务的 [SqlService 类](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) 对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个指定服务的显示名称的字符串值。  
  
## <a name="remarks"></a>注释  
 此字符串的最大长度为 256 个字符。 此名称在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 配置管理器中是区分大小写的。 但是，显示名称比较始终不区分大小写。  
  
## <a name="example"></a>示例  
  
```  
mysqlservice.DisplayName = "Atdisk"  
```  
  
## <a name="see-also"></a>另请参阅  
 [启动和停止服务](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
