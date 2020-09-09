---
description: ExitCode 属性（SqlService 类）
title: 'ExitCode 属性 (SqlService) '
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- ExitCode Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ExitCode property
ms.assetid: e6b8bff2-946f-4abe-bd50-1f7bb11fdddf
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 71e5fbe4180c67560709f004ba099bb90ca83b02
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542837"
---
# <a name="exitcode-property-sqlservice-class"></a>ExitCode 属性（SqlService 类）
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  获取或设置 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Win32 错误代码，它用于定义在启动或停止服务时遇到的问题。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.ExitCode [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *object*  
 一个表示服务的 [SqlService 类](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) 对象。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个指定退出代码的 **uint32** 值。  
  
## <a name="remarks"></a>备注  
 如果错误是此类表示的服务所特有的，则此属性将设置为 ERROR_SERVICE_SPECIFIC_ERROR (1066)。 当服务运行时，将此值设置为 NO_ERROR；而当服务正常终止时，再次将它设置为此值。  
  
## <a name="see-also"></a>另请参阅  
 [启动和停止服务](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
