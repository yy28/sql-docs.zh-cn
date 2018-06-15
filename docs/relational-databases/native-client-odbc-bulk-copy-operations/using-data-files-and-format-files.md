---
title: 使用数据文件和格式文件 |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-bulk-copy-operations
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- bulk copy [ODBC], file formats
- ODBC, functions
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [SQL Server Native Client]
- ODBC, bulk copy operations
- bulk copy [ODBC], data files
ms.assetid: c01b7155-3f0a-473d-90b7-87a97bc56ca5
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 4473473b97545a522ed0a051a69104d2b3d69af8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32946482"
---
# <a name="using-data-files-and-format-files"></a>使用数据文件和格式化文件
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  最简单的大容量复制程序执行以下操作：  
  
1.  调用[bcp_init](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-init.md)指定进行大容量复制 （组 BCP_OUT） 从表或视图拖动到数据文件。  
  
2.  调用[bcp_exec](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-exec.md)执行批量复制操作。  
  
 数据文件以本机模式创建；因此，来自表或视图中所有列的数据都采用与数据库中相同的格式存储于数据文件中。 然后，通过使用与上述相同的步骤并设置 DB_IN（而非 DB_OUT），将该文件大容量复制到某一服务器中。 只有在源表和目标表都具有完全相同的结构时，这一功能才适用。 生成的数据文件也可作为输入的**bcp**实用工具通过使用 **/n** （本机模式） 交换机。  
  
 若要大容量复制出 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句的结果集，而非直接从表或视图复制：  
  
1.  调用**bcp_init**指定大容量复制，但为表名，则指定 NULL。  
  
2.  调用[bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md)与*eOption*设置为 BCPHINTS 和*iValue*设置为指向包含 TRANSACT-SQL 语句的 SQLTCHAR 字符串的指针。  
  
3.  调用**bcp_exec**执行批量复制操作。  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句可以是生成某一结果集的任何语句。 将创建包含 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句的第一个结果集的数据文件。 如果 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句生成多个结果集，则大容量复制将忽略第一个结果集之后的所有结果集。  
  
 若要创建哪一列中数据存储在表中比其他格式数据文件时，调用[bcp_columns](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md)来指定列的数量将会更改，然后调用[bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md)为每个列的格式你想要更改。 这可在调用**bcp_init**但在通过调用**bcp_exec**。 **bcp_colfmt**指定列的数据存储在数据文件的格式。 在大容量复制入或复制出时可以使用该函数。你还可以使用**bcp_colfmt**设置行和列终止符。 例如，如果你的数据中包含没有制表符，你可以创建制表符分隔的文件使用**bcp_colfmt**将制表符设置为每个列的终止符。  
  
 当大容量复制并使用**bcp_colfmt**，你可以轻松创建一个描述已通过调用创建的数据文件的格式文件[bcp_writefmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-writefmt.md)在最后一个调用后**bcp_colfmt**.  
  
 当大容量复制从格式化文件所描述的数据文件中时，通过调用读取格式化文件[bcp_readfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-readfmt.md)后**bcp_init**之前**bcp_exec**。  
  
 **Bcp_control**函数控制多个选项，当大容量复制到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据文件中。 **bcp_control**设置选项，如最大错误在终止之前，在其上开始大容量复制、 行上，停止和批大小的文件中的行数。  
  
## <a name="see-also"></a>另请参阅  
 [执行大容量复制操作&#40;ODBC&#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
  
