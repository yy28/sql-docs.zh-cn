---
title: DisplayName 属性（SqlService 类） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 9439b7410821cffe5d959fda7a894e4f69e33ed0
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85002317"
---
# <a name="displayname-property-sqlservice-class"></a>DisplayName 属性（SqlService 类）
  获取服务的显示名称。  
  
## <a name="syntax"></a>语法  
  
```  
  
object  
.DisplayName [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *object*  
 一个表示服务的 [SqlService 类](sqlservice-class.md) 对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个指定服务的显示名称的字符串值。  
  
## <a name="remarks"></a>备注  
 此字符串的最大长度为 256 个字符。 此名称在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 配置管理器中是区分大小写的。 但是，显示名称比较始终不区分大小写。  
  
## <a name="example"></a>示例  
  
```  
mysqlservice.DisplayName = "Atdisk"  
```  
  
## <a name="see-also"></a>另请参阅  
 [启动和停止服务](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
