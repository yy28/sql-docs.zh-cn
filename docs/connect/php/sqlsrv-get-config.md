---
title: sqlsrv_get_config | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
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
ms.openlocfilehash: 9f7792781b5ead7f0b9a8c035d1282ddd4c4c1e0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
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
  
