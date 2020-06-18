---
title: 为 FILESTREAM 数据创建客户端应用程序 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], Win32
ms.assetid: 8a02aff6-e54c-40c6-a066-2083e9b090aa
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: d7170ff88c0c7c9fd40c372467d2e3fd407a90cf
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84955597"
---
# <a name="create-client-applications-for-filestream-data"></a>为 FILESTREAM 数据创建客户端应用程序
  可以使用 Win32 在 FILESTREAM BLOB 中读取和写入数据。 您需要执行以下步骤：  
  
-   读取 FILESTREAM 文件路径。  
  
-   读取当前事务上下文。  
  
-   获取 Win32 句柄，并使用该句柄在 FILESTREAM BLOB 中读取和写入数据。  
  
> [!NOTE]  
>  本主题中的示例需要在 [创建启用 FILESTREAM 的数据库](create-a-filestream-enabled-database.md) 和 [创建表以存储 FILESTREAM 数据](create-a-table-for-storing-filestream-data.md)中创建的启用了 FILESTREAM 的数据库和表。  
  
##  <a name="functions-for-working-with-filestream-data"></a><a name="func"></a> 用于使用 FILESTREAM 数据的函数  
 使用 FILESTREAM 来存储二进制大型对象 (BLOB) 数据时，可使用 Win32 API 来处理文件。 为了支持在 Win32 应用程序中处理 FILESTREAM BLOB 数据， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供了以下函数和 API：  
  
-   [PathName](/sql/relational-databases/system-functions/pathname-transact-sql) 可将路径作为标记返回给 BLOB。 应用程序可使用此标记来获取 Win32 句柄并对 BLOB 数据进行操作。  
  
     在包含 FILESTREAM 数据的数据库属于某一 AlwaysOn 可用性组时，PathName 函数返回虚拟网络名称 (VNN)，而非计算机名称。  
  
-   [GET_FILESTREAM_TRANSACTION_CONTEXT()](/sql/t-sql/functions/get-filestream-transaction-context-transact-sql) 可返回表示会话当前事务的标记。 应用程序使用此标记可将 FILESTREAM 文件系统流式处理操作绑定到该事务。  
  
-   [OpenSqlFilestream API](access-filestream-data-with-opensqlfilestream.md) 可获取 Win32 文件句柄。 应用程序使用此句柄可对 FILESTREAM 数据进行流式处理，然后可以将此句柄传递给以下 Win32 API： [ReadFile](https://go.microsoft.com/fwlink/?LinkId=86422)、 [WriteFile](https://go.microsoft.com/fwlink/?LinkId=86423)、 [TransmitFile](https://go.microsoft.com/fwlink/?LinkId=86424)、 [SetFilePointer](https://go.microsoft.com/fwlink/?LinkId=86425)、 [SetEndOfFile](https://go.microsoft.com/fwlink/?LinkId=86426)或 [FlushFileBuffers](https://go.microsoft.com/fwlink/?LinkId=86427)。 如果应用程序使用此句柄来调用任何其他 API，则会返回 ERROR_ACCESS_DENIED 错误。 应用程序应使用 [CloseHandle](https://go.microsoft.com/fwlink/?LinkId=86428)来关闭此句柄。  
  
 所有 FILESTREAM 数据容器访问都是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 事务中执行的。 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句以保持 SQL 数据和 FILESTREAM 数据之间的一致性。  
  
##  <a name="steps-for-accessing-filestream-data"></a><a name="steps"></a> 访问 FILESTREAM 数据的步骤  
  
###  <a name="reading-the-filestream-file-path"></a><a name="path"></a> 读取 FILESTREAM 文件路径  
 FILESTREAM 表中的每个单元都具有关联的文件路径。 若要读取该路径，请在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句中使用 `PathName` 列的 `varbinary(max)` 属性。 下面的示例说明了如何读取 `varbinary(max)` 列的文件路径。  
  
 [!code-sql[FILESTREAM#FS_PathName](../../snippets/tsql/SQL15/tsql/filestream/transact-sql/filestream.sql#fs_pathname)]  
  
###  <a name="reading-the-transaction-context"></a><a name="trx"></a> 读取事务上下文  
 要获取当前事务上下文，请使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] [GET_FILESTREAM_TRANSACTION_CONTEXT()](/sql/t-sql/functions/get-filestream-transaction-context-transact-sql) 函数。 下面的示例说明了如何开始执行事务并读取当前事务上下文。  
  
 [!code-sql[FILESTREAM#FS_GET_TRANSACTION_CONTEXT](../../snippets/tsql/SQL15/tsql/filestream/transact-sql/filestream.sql#fs_get_transaction_context)]  
  
###  <a name="obtaining-a-win32-file-handle"></a><a name="handle"></a> 获取 Win32 文件句柄  
 若要获取 Win32 文件句柄，请调用 OpenSqlFilestream API。 此 API 是从 sqlncli.dll 文件中导出的。 可以将返回的句柄传递给以下任何 Win32 API： [ReadFile](https://go.microsoft.com/fwlink/?LinkId=86422)、 [WriteFile](https://go.microsoft.com/fwlink/?LinkId=86423)、 [TransmitFile](https://go.microsoft.com/fwlink/?LinkId=86424)、 [SetFilePointer](https://go.microsoft.com/fwlink/?LinkId=86425)、 [SetEndOfFile](https://go.microsoft.com/fwlink/?LinkId=86426)或 [FlushFileBuffers](https://go.microsoft.com/fwlink/?LinkId=86427)。 下面的示例说明了如何获取 Win32 文件句柄并使用它在 FILESTREAM BLOB 中读取和写入数据。  
  
 [!code-csharp[FILESTREAM#FS_CS_ReadAndWriteBLOB](../../snippets/tsql/SQL15/tsql/filestream/cs/filestream.cs#fs_cs_readandwriteblob)]  
  
 [!code-vb[FILESTREAM#FS_VB_ReadAndWriteBLOB](../../snippets/tsql/SQL15/tsql/filestream/vb/filestream.vb#fs_vb_readandwriteblob)]  
  
 [!code-cpp[FILESTREAM#FS_CPP_WriteBLOB](../../snippets/tsql/SQL15/tsql/filestream/cpp/filestream.cpp#fs_cpp_writeblob)]  
  
##  <a name="best-practices-for-application-design-and-implementation"></a><a name="best"></a> 应用程序设计和实现的最佳实践  
  
-   设计和实现使用 FILESTREAM 的应用程序时，应考虑下列准则：  
  
-   使用 NULL 代替 0x 来表示未初始化的 FILESTREAM 列。 0x 值会导致创建文件，而 NULL 不会。  
  
-   避免在包含非空 FILESTREAM 列的表中执行插入和删除操作。 插入和删除操作会修改用于垃圾收集的 FILESTREAM 表。 这可能导致应用程序的性能随着时间的推移而下降。  
  
-   在使用复制的应用程序中，使用 NEWSEQUENTIALID() 代替 NEWID()。 在这些应用程序中生成 GUID 时，NEWSEQUENTIALID() 比 NEWID() 的性能更好。  
  
-   FILESTREAM API 是专门为了以 Win32 流方式访问数据而设计的。 应避免使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 读取或写入超过 2 MB 的 FILESTREAM 二进制大型对象 (BLOB)。 如果必须从 [!INCLUDE[tsql](../../includes/tsql-md.md)]读取或写入 BLOB 数据，请确保尝试从 Win32 打开 FILESTREAM BLOB 之前所有的 BLOB 数据都已占用。 无法占用所有的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 数据可能会导致任何后续的 FILESTREAM 打开或关闭操作失败。  
  
-   避免使用向 FILESTREAM BLOB 中更新、追加或预置数据的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句。 这会导致 BLOB 数据被假脱机保存到 tempdb 数据库中，然后回到新物理文件中。  
  
-   避免将小型 BLOB 更新追加到 FILESTREAM BLOB 中。 每次追加都会导致复制基础 FILESTREAM 文件。 如果应用程序必须追加小型 BLOB，请将 BLOB 写入 `varbinary(max)` 列，然后在 BLOB 数达到预设的限制时对 FILESTREAM BLOB 执行单次写入操作。  
  
-   避免在应用程序中检索大量 BLOB 文件的数据长度。 这是非常耗时的操作，因为大小未存储在 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]中。 如果必须确定 BLOB 文件的长度，请使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] DATALENGTH() 函数确定 BLOB 的大小（如果它是关闭的）。 DATALENGTH() 不会打开 BLOB 文件来确定其大小。  
  
-   如果应用程序使用 Message Block1 (SMB1) 协议，则应以 60 KB 的倍数读取 FILESTREAM BLOB 数据以优化性能。  
  
## <a name="see-also"></a>另请参阅  
 [避免与 FILESTREAM 应用程序中的数据库操作冲突](avoid-conflicts-with-database-operations-in-filestream-applications.md)   
 [使用 OpenSqlFilestream 访问 FILESTREAM 数据](access-filestream-data-with-opensqlfilestream.md)   
 [二进制大型对象 &#40;Blob&#41; 数据 &#40;SQL Server&#41;](binary-large-object-blob-data-sql-server.md)   
 [对 FILESTREAM 数据进行部分更新](make-partial-updates-to-filestream-data.md)  
  
  
