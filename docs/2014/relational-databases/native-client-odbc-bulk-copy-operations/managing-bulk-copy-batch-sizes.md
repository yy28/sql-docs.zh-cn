---
title: 管理大容量复制批大小 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, bulk copy
- ODBC, bulk copy operations
- batches [ODBC]
- bulk copy [ODBC], batch sizes
ms.assetid: 4b24139f-788b-45a6-86dc-ae835435d737
caps.latest.revision: 31
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 02f03c1d7c050044e77b9f1946d974c264b5cac0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36027670"
---
# <a name="managing-bulk-copy-batch-sizes"></a>管理大容量复制的批大小
  在大容量复制操作中，批的主要目的在于定义事务的范围。 如果没有设置批大小，则大容量复制函数会将整个大容量复制视为一个事务。 如果设置了批大小，则每个批构成一个事务，当批运行完成时，该事务也就被提交。  
  
 如果在没有指定批大小的情况下执行大容量复制并且遇到错误，则将回滚整个大容量复制。 恢复长时间运行的大容量复制可能需要花费很长的时间。 如果设置了批大小，则大容量复制将每个批视为一个事务并分别提交每个批。 如果遇到错误，只需回滚最后一个未完成的批。  
  
 此外，批大小还会影响锁定开销。 执行针对大容量复制时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，可以使用指定 TABLOCK 提示[bcp_control](../native-client-odbc-extensions-bulk-copy-functions/bcp-control.md)获取表锁而不是行锁。 对于整个大容量复制操作而言，持有单个表锁的开销最小。 如果未指定 TABLOCK，则对各个行持有锁，并且在大容量复制操作期间维护所有锁的开销会导致性能降低。 由于仅在事务执行期间才持有锁，因而可以通过指定批大小来解决此问题，因为这样可以定期生成能够释放当前持有的锁的提交。  
  
 如果要大容量复制大量的行，构成批的行的数目会对性能产生显著影响。 建议采用的批大小取决于要执行的大容量复制的类型。  
  
-   在对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进行大容量复制时，请指定 TABLOCK 大容量复制提示并设置一个较大的批大小。  
  
-   如果不指定 TABLOCK，请将批大小限制为小于 1,000 行。  
  
 当大容量复制从数据文件中时，通过调用指定批次大小**bcp_control**使用之前调用 BCPBATCH 选项[bcp_exec](../native-client-odbc-extensions-bulk-copy-functions/bcp-exec.md)。 当大容量复制从程序变量使用[bcp_bind](../native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)和[bcp_sendrow](../native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md)，批大小控制通过调用[bcp_batch](../native-client-odbc-extensions-bulk-copy-functions/bcp-batch.md)之后调用[bcp_sendrow](../native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md) *x*时间 where *x*是批处理中的行数。  
  
 除了指定事务大小之外，批还会影响将行通过网络发送到服务器的时间。 大容量复制函数通常缓存中的行**bcp_sendrow**网络数据包填满，然后将完整的数据包发送到服务器之前。 在应用程序调用**bcp_batch**，但是，当前的数据包发送到无论是否具有已填充的服务器。 使用很小的批大小可能导致向服务器发送许多部分填满的数据包，从而降低性能。 例如，调用**bcp_batch**后每个**bcp_sendrow**导致每个要在单独的数据包中发送的行，并且，除非的行是非常大，浪费了每个数据包中的空间。 SQL Server 的网络数据包的默认大小为 4 KB，尽管应用程序可以通过调用来更改大小[SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md)指定 SQL_ATTR_PACKET_SIZE 特性。  
  
 批处理的另一个副作用是每个批处理被视为未完成的结果集之前已完成并且**bcp_batch**。 如果未完成，一批时，任何其他操作会尝试连接句柄上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序问题 SQLState 错误 ="HY000"和错误消息字符串的：  
  
```  
"[Microsoft][SQL Server Native Client] Connection is busy with  
results for another hstmt."  
```  
  
## <a name="see-also"></a>请参阅  
 [执行大容量复制操作&#40;ODBC&#41;](performing-bulk-copy-operations-odbc.md)   
 [批量导入和导出数据 (SQL Server)](../import-export/bulk-import-and-export-of-data-sql-server.md)  
  
  