---
title: sqlsrv_get_config | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- sqlsrv_get_config
apitype: NA
helpviewer_keywords:
- API Reference, sqlsrv_get_config
- sqlsrv_get_config
ms.assetid: ce2befc2-af98-45bb-8d41-60f1674dccfc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f94c20c8aa6cf603c6588586e072813682b2ce68
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "67992698"
---
# <a name="sqlsrv_get_config"></a>sqlsrv_get_config
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

返回指定配置设置的当前值。  
  
## <a name="syntax"></a>语法  
  
```  
  
sqlsrv_get_config( string $setting )  
```  
  
#### <a name="parameters"></a>parameters  
*$setting*：为其返回该值的配置设置。 有关可配置设置的列表，请参阅 [sqlsrv_configure](../../connect/php/sqlsrv-configure.md)。  
  
## <a name="return-value"></a>返回值  
*$setting* 参数指定的设置的值。 如果指定的设置无效，将返回 **false** ，并向错误集合中添加一个错误。  
  
## <a name="remarks"></a>备注  
如果 **false** config **sqlsrv_get_config**，必须调用 [sqlsrv_errors](../../connect/php/sqlsrv-errors.md) 来确定是否发生错误，或 **false** 是否是 *$setting* 参数指定的设置的值。  
  
## <a name="see-also"></a>另请参阅  
[SQLSRV 驱动程序 API 参考](../../connect/php/sqlsrv-driver-api-reference.md)  

[sqlsrv_configure](../../connect/php/sqlsrv-configure.md)  

[sqlsrv_errors](../../connect/php/sqlsrv-errors.md)  
  
