---
title: sqlsrv_get_config | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- sqlsrv_get_config
apitype: NA
helpviewer_keywords:
- API Reference, sqlsrv_get_config
- sqlsrv_get_config
ms.assetid: ce2befc2-af98-45bb-8d41-60f1674dccfc
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 433f5dc1d997c4f8756ad48a446aebff977cb908
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsrvgetconfig"></a>sqlsrv_get_config
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

返回指定配置设置的当前值。  
  
## <a name="syntax"></a>语法  
  
```  
  
sqlsrv_get_config( string $setting )  
```  
  
#### <a name="parameters"></a>Parameters  
*$setting*：为其返回该值的配置设置。 有关可配置设置的列表，请参阅 [sqlsrv_configure](../../connect/php/sqlsrv-configure.md)。  
  
## <a name="return-value"></a>返回值  
*$setting* 参数指定的设置的值。 如果指定的设置无效，将返回 **false** ，并向错误集合中添加一个错误。  
  
## <a name="remarks"></a>注释  
如果 **false** config **sqlsrv_get_config**，必须调用 [sqlsrv_errors](../../connect/php/sqlsrv-errors.md) 来确定是否发生错误，或 **false** 是否是 *$setting* 参数指定的设置的值。  
  
## <a name="see-also"></a>另请参阅  
[SQLSRV 驱动程序 API 参考](../../connect/php/sqlsrv-driver-api-reference.md)  

[sqlsrv_configure](../../connect/php/sqlsrv-configure.md)  

[sqlsrv_errors](../../connect/php/sqlsrv-errors.md)  
  
