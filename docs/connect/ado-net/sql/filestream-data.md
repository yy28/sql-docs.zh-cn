---
title: FILESTREAM 数据
description: 介绍如何使用 FILESTREAM 属性处理 SQL Server 2008 中存储的大值数据。
ms.date: 08/15/2019
ms.assetid: bd8b845c-0f09-4295-b466-97ef106eefa8
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: e3e26a76522d1c1a99794076c5f152e6ec1e1f7d
ms.sourcegitcommit: 610e49c3e1fa97056611a85e31e06ab30fd866b1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/07/2020
ms.locfileid: "78896744"
---
# <a name="filestream-data"></a>FILESTREAM 数据

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

FILESTREAM 存储属性可用于 varbinary(max) 列中存储的二进制 (BLOB) 数据。 在使用 FILESTREAM 之前，存储二进制数据需要经过特殊处理。 非结构化数据（例如文本文档、图像和视频）通常存储在数据库外部，因此难以管理。

> [!NOTE]
> 必须安装 .NET Framework 3.5 SP1（或更高版本）或 .NET Core 才能使用 SqlClient 处理 FILESTREAM 数据。

在 varbinary(max) 列上指定 FILESTREAM 特性会致使 SQL Server 将数据存储在本地 NTFS 文件系统中，而不是存储在数据库文件中。 虽然数据是单独存储的，但可以使用受支持的相同 Transact-SQL 语句处理存储在数据库中的 varbinary(max) 数据。

## <a name="sqlclient-support-for-filestream"></a>SqlClient 对 FILESTREAM 的支持

适用于 SQL Server 的 Microsoft SqlClient 数据提供程序 (<xref:Microsoft.Data.SqlClient>) 支持使用在 <xref:System.Data.SqlTypes> 命名空间中定义的 <xref:Microsoft.Data.SqlTypes.SqlFileStream> 类来读写 FILESTREAM 数据。 `SqlFileStream` 继承自 <xref:System.IO.Stream> 类，该类提供了用于读写数据流的方法。 从流中读取会将数据从流传输到数据结构（如字节数组）中。 写入数据会将数据从数据结构传输到流中。

### <a name="creating-the-sql-server-table"></a>创建 SQL Server 表

下列 Transact-SQL 语句将创建一个名为 employees 的表并插入一行数据。 启用 FILESTREAM 存储后，可以将此表与下面的代码示例结合使用。 本主题末尾提供了 SQL Server 联机丛书中资源的链接。

```sql
CREATE TABLE employees
(
  EmployeeId INT  NOT NULL  PRIMARY KEY,
  Photo VARBINARY(MAX) FILESTREAM  NULL,
  RowGuid UNIQUEIDENTIFIER  NOT NULL  ROWGUIDCOL
  UNIQUE DEFAULT NEWID()
)
GO
Insert into employees
Values(1, 0x00, default)
GO
```

### <a name="example-reading-overwriting-and-inserting-filestream-data"></a>示例：读取、覆盖和插入 FILESTREAM 数据

下面的示例演示如何从 FILESTREAM 读取数据。 该代码获取文件的逻辑路径，将 `FileAccess` 设置为 `Read`，并将 `FileOptions` 设置为 `SequentialScan`。 然后，该代码将 SqlFileStream 中的字节读取到缓冲区中。 然后，将字节写入控制台窗口。

该示例还演示了如何将数据写入到 FILESTREAM（其中现有的所有数据将被覆盖）。 该代码获取文件的逻辑路径，并创建 `SqlFileStream`，将 `FileAccess` 设置为 `Write`，将 `FileOptions` 设置为 `SequentialScan`。 将一个字节写入 `SqlFileStream`，替换文件中的所有数据。

示例还演示了如何通过使用 Seek 方法将数据附加到 FILESTREAM 文件的结尾，以将数据写入到其中。 该代码获取文件的逻辑路径，并创建 `SqlFileStream`，将 `FileAccess` 设置为 `ReadWrite`，将 `FileOptions` 设置为 `SequentialScan`。 此代码使用 Seek 方法查找到文件的末尾，并向现有文件追加一个字节。

```csharp
using System;
using Microsoft.Data.SqlClient;
using System.Data.SqlTypes;
using System.Data;
using System.IO;

namespace FileStreamTest
{
    class Program
    {
        static void Main(string[] args)
        {
            SqlConnectionStringBuilder builder = new SqlConnectionStringBuilder("server=(local);integrated security=true;database=myDB");
            ReadFileStream(builder);
            OverwriteFileStream(builder);
            InsertFileStream(builder);

            Console.WriteLine("Done");
        }

        private static void ReadFileStream(SqlConnectionStringBuilder connStringBuilder)
        {
            using (SqlConnection connection = new SqlConnection(connStringBuilder.ToString()))
            {
                connection.Open();
                SqlCommand command = new SqlCommand("SELECT TOP(1) Photo.PathName(), GET_FILESTREAM_TRANSACTION_CONTEXT() FROM employees", connection);

                SqlTransaction tran = connection.BeginTransaction(IsolationLevel.ReadCommitted);
                command.Transaction = tran;

                using (SqlDataReader reader = command.ExecuteReader())
                {
                    while (reader.Read())
                    {
                        // Get the pointer for the file
                        string path = reader.GetString(0);
                        byte[] transactionContext = reader.GetSqlBytes(1).Buffer;

                        // Create the SqlFileStream
                        using (Stream fileStream = new SqlFileStream(path, transactionContext, FileAccess.Read, FileOptions.SequentialScan, allocationSize: 0))
                        {
                            // Read the contents as bytes and write them to the console
                            for (long index = 0; index < fileStream.Length; index++)
                            {
                                Console.WriteLine(fileStream.ReadByte());
                            }
                        }
                    }
                }
                tran.Commit();
            }
        }

        private static void OverwriteFileStream(SqlConnectionStringBuilder connStringBuilder)
        {
            using (SqlConnection connection = new SqlConnection(connStringBuilder.ToString()))
            {
                connection.Open();

                SqlCommand command = new SqlCommand("SELECT TOP(1) Photo.PathName(), GET_FILESTREAM_TRANSACTION_CONTEXT() FROM employees", connection);

                SqlTransaction tran = connection.BeginTransaction(IsolationLevel.ReadCommitted);
                command.Transaction = tran;

                using (SqlDataReader reader = command.ExecuteReader())
                {
                    while (reader.Read())
                    {
                        // Get the pointer for file
                        string path = reader.GetString(0);
                        byte[] transactionContext = reader.GetSqlBytes(1).Buffer;

                        // Create the SqlFileStream
                        using (Stream fileStream = new SqlFileStream(path, transactionContext, FileAccess.Write, FileOptions.SequentialScan, allocationSize: 0))
                        {
                            // Write a single byte to the file. This will
                            // replace any data in the file.
                            fileStream.WriteByte(0x01);
                        }
                    }
                }
                tran.Commit();
            }
        }

        private static void InsertFileStream(SqlConnectionStringBuilder connStringBuilder)
        {
            using (SqlConnection connection = new SqlConnection(connStringBuilder.ToString()))
            {
                connection.Open();

                SqlCommand command = new SqlCommand("SELECT TOP(1) Photo.PathName(), GET_FILESTREAM_TRANSACTION_CONTEXT() FROM employees", connection);

                SqlTransaction tran = connection.BeginTransaction(IsolationLevel.ReadCommitted);
                command.Transaction = tran;

                using (SqlDataReader reader = command.ExecuteReader())
                {
                    while (reader.Read())
                    {
                        // Get the pointer for file
                        string path = reader.GetString(0);
                        byte[] transactionContext = reader.GetSqlBytes(1).Buffer;

                        using (Stream fileStream = new SqlFileStream(path, transactionContext, FileAccess.ReadWrite, FileOptions.SequentialScan, allocationSize: 0))
                        {
                            // Seek to the end of the file
                            fileStream.Seek(0, SeekOrigin.End);

                            // Append a single byte
                            fileStream.WriteByte(0x01);
                        }
                    }
                }
                tran.Commit();
            }

        }
    }
}
```

关于另一个示例，请参见[如何将二进制数据存储和提取到文件流列中](https://www.codeproject.com/Articles/32216/How-to-store-and-fetch-binary-data-into-a-file-str)。

## <a name="resources-in-sql-server-books-online"></a>SQL Server 联机丛书中的资源

FILESTREAM 的完整文档位于 SQL Server 联机丛书中的以下各节中。

|主题|说明|
|-----------|-----------------|
|[FILESTREAM (SQL Server)](../../../relational-databases/blob/filestream-sql-server.md)|介绍何时使用 FILESTREAM 存储以及它如何将 SQL Server 数据库引擎与 NTFS 文件系统集成。|
|[为 FILESTREAM 数据创建客户端应用程序](../../../relational-databases/blob/create-client-applications-for-filestream-data.md)|介绍用于处理 FILESTREAM 数据的 Windows API 函数。|
|[FILESTREAM 与其他 SQL Server 功能](../../../relational-databases/blob/filestream-compatibility-with-other-sql-server-features.md)|提供将 FILESTREAM 数据与 SQL Server 的其他功能一起使用时的注意事项、准则和限制。|

## <a name="next-steps"></a>后续步骤
- [SQL Server 数据类型和 ADO.NET](sql-server-data-types.md)
- [SQL Server 二进制和大值数据](sql-server-binary-large-value-data.md)
