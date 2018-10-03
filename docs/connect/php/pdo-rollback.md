---
title: 'Pdo:: rollback |Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d918c1e3-1be0-4001-b3b0-000db6d9e8b8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2f5f33f7d027a858bdd57aa69c65107ed15856e2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47609238"
---
# <a name="pdorollback"></a>PDO::rollback
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

放弃在调用 [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) 后发布的数据库命令，并将连接返回到音频提交模式。  
  
## <a name="syntax"></a>语法  
  
```  
  
bool PDO::rollBack ();  
```  
  
## <a name="return-value"></a>返回值  
如果方法调用成功，则为 True；否则为 False。  
  
## <a name="remarks"></a>Remarks  
PDO::rollback 不受 PDO::ATTR_AUTOCOMMIT 的值影响（也不影响该值）。  
  
有关使用 PDO::rollback 的示例，请参阅 [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) 。  
  
已在 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的版本 2.0 中添加了对 PDO 的支持。  
  
## <a name="see-also"></a>另请参阅  
[PDO 类](../../connect/php/pdo-class.md)

[PDO](http://php.net/manual/book.pdo.php)  
  
