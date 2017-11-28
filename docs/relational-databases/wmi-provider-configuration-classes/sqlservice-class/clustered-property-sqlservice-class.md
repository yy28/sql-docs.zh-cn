---
title: "群集属性 （SqlService 类） |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Clustered Property (SqlService Class)
apilocation: sqlmgmproviderxpsp2up.mof
helpviewer_keywords: Clustered property
ms.assetid: f714e7f5-c2db-45c6-9536-6ca2cb5b42aa
caps.latest.revision: "35"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5f86c229aa422a01f02af4f94fbff5526fb27a04
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="clustered-property-sqlservice-class"></a>Clustered 属性（SqlService 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]获取用于指定服务是否为群集实例的一部分的布尔属性值。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.Clustered [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *对象*  
 一个表示服务的 [SqlService 类](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) 对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个指定服务是否参与群集实例的布尔值：如果服务参与群集实例，则为 **true** ；如果服务不参与群集实例，则为 **false** 。  
  
## <a name="remarks"></a>注释  
  
## <a name="see-also"></a>另请参阅  
 [启动和停止服务](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
