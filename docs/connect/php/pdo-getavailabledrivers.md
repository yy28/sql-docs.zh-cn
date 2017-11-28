---
title: "Pdo:: getavailabledrivers |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: php
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: eab561e6-1229-401a-9482-008c23f9a4e6
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9e76797d64d63fb768886bffe2fb877709355ad2
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
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
  
## <a name="remarks"></a>注释  
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
[PDO](http://go.microsoft.com/fwlink/?LinkID=187441)  
  
