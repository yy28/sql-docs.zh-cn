---
title: "Pdo:: rollback |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d918c1e3-1be0-4001-b3b0-000db6d9e8b8
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6b0ef351838defa86dee7818727a0d538b3e071a
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="pdorollback"></a>PDO::rollback
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

放弃在调用 [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) 后发布的数据库命令，并将连接返回到音频提交模式。  
  
## <a name="syntax"></a>语法  
  
```  
  
bool PDO::rollBack ();  
```  
  
## <a name="return-value"></a>返回值  
如果方法调用成功，则为 True，否则为 False。  
  
## <a name="remarks"></a>注释  
PDO::rollback 不受 PDO::ATTR_AUTOCOMMIT 的值影响（也不影响该值）。  
  
有关使用 PDO::rollback 的示例，请参阅 [PDO::beginTransaction](../../connect/php/pdo-begintransaction.md) 。  
  
已在 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]的版本 2.0 中添加了对 PDO 的支持。  
  
## <a name="see-also"></a>另请参阅  
[PDO 类](../../connect/php/pdo-class.md)  
[PDO](http://go.microsoft.com/fwlink/?LinkID=187441)  
  

