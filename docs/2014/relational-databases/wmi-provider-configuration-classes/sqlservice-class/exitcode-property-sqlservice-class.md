---
title: ExitCode 属性（SqlService 类） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- ExitCode Property (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- ExitCode property
ms.assetid: e6b8bff2-946f-4abe-bd50-1f7bb11fdddf
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f7f5414afd8507a1fc9c592d6b8226692e9683a0
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85002199"
---
# <a name="exitcode-property-sqlservice-class"></a>ExitCode 属性（SqlService 类）
  获取或设置 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Win32 错误代码，它用于定义在启动或停止服务时遇到的问题。  
  
## <a name="syntax"></a>语法  
  
```  
  
object  
.ExitCode [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *object*  
 一个表示服务的 [SqlService 类](sqlservice-class.md) 对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个指定退出代码的 `uint32` 值。  
  
## <a name="remarks"></a>备注  
 如果错误是此类表示的服务所特有的，则此属性将设置为 ERROR_SERVICE_SPECIFIC_ERROR (1066)。 当服务运行时，将此值设置为 NO_ERROR；而当服务正常终止时，再次将它设置为此值。  
  
## <a name="see-also"></a>另请参阅  
 [启动和停止服务](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
