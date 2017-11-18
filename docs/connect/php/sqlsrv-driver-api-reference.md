---
title: "SQLSRV 驱动程序 API 参考 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0b55da26-ddeb-4e89-872a-91e0aba57103
caps.latest.revision: 42
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2bd1cf731f49119e54fb9e5a548a8988af1ef9fc
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsrv-driver-api-reference"></a>SQLSRV 驱动程序 API 参考
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

在 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 中，SQLSRV 驱动程序的 API 名称为 **sqlsrv**。 所有**sqlsrv**函数开头**sqlsrv_**后, 跟谓词或名词。 后跟谓词的函数可执行特定操作，后跟名词的函数可返回特定形式的元数据。  
  
## <a name="in-this-section"></a>本节内容  
SQLSRV 驱动程序包含以下函数：  
  
|函数|Description|  
|------------|---------------|  
|[sqlsrv_begin_transaction](../../connect/php/sqlsrv-begin-transaction.md)|开始一个事务。|  
|[sqlsrv_cancel](../../connect/php/sqlsrv-cancel.md)|取消语句；丢弃该语句的所有挂起结果。|  
|[sqlsrv_client_info](../../connect/php/sqlsrv-client-info.md)|提供有关客户端的信息。|  
|[sqlsrv_close](../../connect/php/sqlsrv-close.md)|关闭连接。 释放与该连接相关联的所有资源。|  
|[sqlsrv_commit](../../connect/php/sqlsrv-commit.md)|提交事务。|  
|[sqlsrv_configure](../../connect/php/sqlsrv-configure.md)|更改错误处理和日志记录配置。|  
|[sqlsrv_connect](../../connect/php/sqlsrv-connect.md)|创建并打开一个连接。|  
|[sqlsrv_errors](../../connect/php/sqlsrv-errors.md)|返回有关最后一次操作的错误和/或警告信息。|  
|[sqlsrv_execute](../../connect/php/sqlsrv-execute.md)|执行已准备的语句。|  
|[sqlsrv_fetch](../../connect/php/sqlsrv-fetch.md)|使下一个数据行可供读取。|  
|[sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md)|将下一个数据行作为数字索引的阵列、关联阵列或这两种阵列进行检索。|  
|[sqlsrv_fetch_object](../../connect/php/sqlsrv-fetch-object.md)|将下一个数据行作为一个对象进行检索。|  
|[sqlsrv_field_metadata](../../connect/php/sqlsrv-field-metadata.md)|sqlsrv_field_metadata。|  
|[sqlsrv_free_stmt](../../connect/php/sqlsrv-free-stmt.md)|关闭语句。 释放与该语句相关联的所有资源。|  
|[sqlsrv_get_config](../../connect/php/sqlsrv-get-config.md)|返回指定配置设置的值。|  
|[sqlsrv_get_field](../../connect/php/sqlsrv-get-field.md)|按索引检索当前行中的字段。 可以指定 PHP 返回类型。|  
|[sqlsrv_has_rows](../../connect/php/sqlsrv-has-rows.md)|检测结果集有一个行还是有多个行。|  
|[sqlsrv_next_result](../../connect/php/sqlsrv-next-result.md)|使下一个结果可供处理。|  
|[sqlsrv_num_rows](../../connect/php/sqlsrv-num-rows.md)|报告结果集中的行数。|  
|[sqlsrv_num_fields](../../connect/php/sqlsrv-num-fields.md)|检索活动结果集中的字段数目。|  
|[sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md)|准备但不执行 TRANSACT-SQL 查询。 隐式绑定参数。|  
|[sqlsrv_query](../../connect/php/sqlsrv-query.md)|准备并执行 Transact-SQL 查询。|  
|[sqlsrv_rollback](../../connect/php/sqlsrv-rollback.md)|回退事务。|  
|[sqlsrv_rows_affected](../../connect/php/sqlsrv-rows-affected.md)|返回修改行的数目。|  
|[sqlsrv_send_stream_data](../../connect/php/sqlsrv-send-stream-data.md)|每次调用该函数时，都可以将最多 8 个字节 (8 KB) 的数据发送到服务器。|  
|[sqlsrv_server_info](../../connect/php/sqlsrv-server-info.md)|提供有关服务器的信息。|  
  
## <a name="reference"></a>参考  
[PHP 手册](http://go.microsoft.com/fwlink/?LinkId=105500)  
  
## <a name="see-also"></a>另请参阅  
[PHP SQL 驱动程序概述](../../connect/php/overview-of-the-php-sql-driver.md)
[常量 &#40;Microsoft Drivers for PHP for SQL server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  
[PHP SQL 驱动程序编程指南](../../connect/php/programming-guide-for-php-sql-driver.md)
[PHP SQL 驱动程序入门](../../connect/php/getting-started-with-the-php-sql-driver.md)
  

