---
title: AcceptPause 属性（SqlService）
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- AcceptPause Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
helpviewer_keywords:
- AcceptPause property
ms.assetid: 4339e903-35ee-4395-b005-ca58b3a24a84
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 80e68dada9ec917ed6c47d0ab1e38e6e608ce209
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85888426"
---
# <a name="acceptpause-property-sqlservice-class"></a>AcceptPause 属性（SqlService 类）
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  获取用于指定是否可以暂停服务的布尔值属性。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.AcceptPause [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *object*  
 一个表示服务的 [SqlService 类](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) 对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个指定是否可以暂停服务的布尔值属性。 如果可以暂停服务，则为**true** ；如果不能暂停服务，则为 **false** 。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [启动和停止服务](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
