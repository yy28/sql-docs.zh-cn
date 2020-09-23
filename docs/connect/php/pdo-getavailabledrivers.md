---
title: PDO::getAvailableDrivers
description: Microsoft PDO_SQLSRV Driver for PHP for SQL Server 中 PDO::getAvailableDrivers 函数的 API 参考。
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: eab561e6-1229-401a-9482-008c23f9a4e6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e43ef53820d24128d16ee0f0c7a5d6f1077ff6d2
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "88646614"
---
# <a name="pdogetavailabledrivers"></a>PDO::getAvailableDrivers
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

在 PHP 安装中返回 PDO 驱动程序的数组。  
  
## <a name="syntax"></a>语法  
  
```  
  
array PDO::getAvailableDrivers ();  
```  
  
## <a name="return-value"></a>返回值  
带有 PDO 驱动程序列表的数组。  
  
## <a name="remarks"></a>注解  
在 PDO::__construct 中使用 PDO 驱动程序的名称来创建 PDO 实例。  
  
PDO::getAvailableDrivers 不需要由 PHP 驱动程序来实现。 有关此方法的详细信息，请参阅 PHP 文档。  
  
已在 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的版本 2.0 中添加了对 PDO 的支持。  
  
## <a name="example"></a>示例  
  
```  
<?php  
print_r(PDO::getAvailableDrivers());  
?>  
```  
  
## <a name="see-also"></a>另请参阅  
[PDO 类](../../connect/php/pdo-class.md)

[PDO](https://php.net/manual/book.pdo.php)  
  
