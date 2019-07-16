---
title: 使用数据文件和格式化文件 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- bulk copy [ODBC], file formats
- ODBC, functions
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [SQL Server Native Client]
- ODBC, bulk copy operations
- bulk copy [ODBC], data files
ms.assetid: c01b7155-3f0a-473d-90b7-87a97bc56ca5
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2fae3c62d923d2e52fd454493b7d1218608b233e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68134245"
---
# <a name="using-data-files-and-format-files"></a>使用数据文件和格式化文件
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  最简单的大容量复制程序执行以下操作：  
  
1.  调用[bcp_init](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-init.md)指定外大容量复制 （设置 BCP_OUT） 从表或视图拖动到数据文件。  
  
2.  调用[bcp_exec](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-exec.md)以执行大容量复制操作。  
  
 数据文件以本机模式创建；因此，来自表或视图中所有列的数据都采用与数据库中相同的格式存储于数据文件中。 然后，通过使用与上述相同的步骤并设置 DB_IN（而非 DB_OUT），将该文件大容量复制到某一服务器中。 只有在源表和目标表都具有完全相同的结构时，这一功能才适用。 生成的数据文件还可以输入到**bcp**实用工具中使用 **/n** （本机模式） 开关。  
  
 若要大容量复制出 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句的结果集，而非直接从表或视图复制：  
  
1.  调用**bcp_init**指定大容量复制出，但表名称指定为 NULL。  
  
2.  调用[bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md)与*eOption*设置为 BCPHINTS 并*iValue*设置为指向包含 TRANSACT-SQL 语句的 SQLTCHAR 字符串的指针。  
  
3.  调用**bcp_exec**以执行大容量复制操作。  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句可以是生成某一结果集的任何语句。 将创建包含 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句的第一个结果集的数据文件。 如果 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句生成多个结果集，则大容量复制将忽略第一个结果集之后的所有结果集。  
  
 若要创建哪一列中数据存储在不同的格式比表中的数据文件，请调用[bcp_columns](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md)若要指定将更改多少列，然后调用[bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md)的每个列的格式你想要更改。 这是之后调用**bcp_init**但在通过调用**bcp_exec**。 **bcp_colfmt**指定列的数据存储在数据文件的格式。 大容量复制入或签出时可以使用它。此外可以使用**bcp_colfmt**设置行和列终止符。 例如，如果数据不包含任何制表符，您可以创建制表符分隔文件通过使用**bcp_colfmt**将制表符设置为每个列的终止符。  
  
 当大容量复制和使用**bcp_colfmt**，可以轻松创建描述已通过调用创建的数据文件的格式文件[bcp_writefmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-writefmt.md)在最后一个调用**bcp_colfmt**.  
  
 当大容量复制中所述的格式化文件将数据文件中时，通过调用读取格式化文件[bcp_readfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-readfmt.md)后**bcp_init**之前**bcp_exec**。  
  
 **Bcp_control**函数控制多个选项时大容量复制到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]从数据文件。 **bcp_control**设置一些选项，如终止前的错误，在其上开始大容量复制、 要在其停止的行和批大小的文件中的行的最大数目。  
  
## <a name="see-also"></a>请参阅  
 [执行大容量复制操作&#40;ODBC&#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)  
  
  
