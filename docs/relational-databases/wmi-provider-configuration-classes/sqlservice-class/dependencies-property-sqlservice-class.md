---
title: 依赖项属性（SqlService）
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- Dependencies Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- Dependencies property
ms.assetid: 92d54b7e-de2f-4978-b601-0196e37cbb41
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 993c922562773648aac5460116ba6e343a72132f
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/06/2019
ms.locfileid: "73659277"
---
# <a name="dependencies-property-sqlservice-class"></a>Dependencies 属性（SqlService 类）
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  获取依赖于所引用服务的服务列表。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.Dependencies [= value]  
```  
  
## <a name="parts"></a>组成部分  
 对象  
 一个表示服务的 [SqlService 类](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) 对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个包含依赖于所引用服务的服务列表的字符串数组。  
  
## <a name="remarks"></a>注释  
  
## <a name="see-also"></a>另请参阅  
 [启动和停止服务](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
