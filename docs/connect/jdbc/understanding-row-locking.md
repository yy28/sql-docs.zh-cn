---
title: "了解行锁定 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 63c76a2f-f2b9-461f-8904-acbda0169ac3
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7b41b33aa022bc0a62996e09a713f36bbe04e816
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="understanding-row-locking"></a>了解行锁定
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]行锁。 这样，就可以在同时在数据库中执行修改的多个用户之间实施并发控制。 默认情况下，事务和锁是在每个连接的基础上进行管理的。 例如，如果应用程序打开两个 JDBC 连接，则一个连接获得的锁不能与另一个连接共享。 一个连接所获得的锁不能与另一个连接所持有的锁相冲突。  
  
> [!NOTE]  
>  如果使用行锁定，则将锁定提取缓冲区中的所有行，这样，如果提取大小的设置非常大，则可能影响并发性能。  
  
 锁定用于确保事务完整性和数据库一致性。 锁定可以防止用户读取其他用户正在更改的数据，并防止多个用户同时更改相同的数据。 如果不使用锁定，数据库中的数据可能在逻辑上变得不正确，而针对这些数据进行查询可能会产生想不到的结果。  
  
> [!NOTE]  
>  有关详细信息行中的锁定有关[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]，请参阅"中的锁定[!INCLUDE[ssDE](../../includes/ssde_md.md)]"中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]联机丛书。  
  
## <a name="see-also"></a>另请参阅  
 [使用 JDBC 驱动程序管理结果集](../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md)  
  
  

