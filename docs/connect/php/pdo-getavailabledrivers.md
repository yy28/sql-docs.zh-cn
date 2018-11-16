---
title: 'Pdo:: getavailabledrivers |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: eab561e6-1229-401a-9482-008c23f9a4e6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a8e34675ccd92ae714117a41198518cb7ec28afb
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 11/13/2018
ms.locfileid: "51604847"
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
  
## <a name="remarks"></a>Remarks  
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
  
