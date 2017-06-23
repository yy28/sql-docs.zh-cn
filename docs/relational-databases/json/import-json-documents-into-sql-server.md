---
title: "将 JSON 文档导入 SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0e908ec0-7173-4cd2-8f48-2700757b53a5
caps.latest.revision: 5
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 439b568fb268cdc6e6a817f36ce38aeaeac11fab
ms.openlocfilehash: 1c842fde925e89901971a525c3e171ffce050269
ms.contentlocale: zh-cn
ms.lasthandoff: 06/23/2017

---
# <a name="import-json-documents-into-sql-server"></a>将 JSON 文档导入 SQL Server
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

本主题介绍如何导入 SQL Server 的 JSON 文件。 当前有存储在文件中的 JSON 文档的很多。 应用程序记录 JSON 文件中的信息、 传感器生成的存储在 JSON 文件等的信息。 必须能够读取文件中存储的 JSON 数据、将数据载入 SQL Server 和分析数据。

## <a name="import-a-json-document-into-a-single-column"></a>将 JSON 文档导入单个列
**OPENROWSET(BULK)** 是一个表值函数，如果 SQL Server 对本地驱动器或网络中的任一文件拥有读取访问权限，则该函数可从该文件中读取数据。 该函数返回包含单个列的表，该列包含文件的内容。 可以结合 OPENROWSET(BULK) 函数使用各种选项，例如分隔符。 但是，最简单的用法是将整个文件内容作为文本值加载。 （这单个大型值称为单字符大型对象或 SINGLE_CLOB。） 

下面的示例 **OPENROWSET(BULK)** 函数读取 JSON 文件的内容，然后以单个值的形式将该内容返回给用户：

```sql
SELECT BulkColumn
 FROM OPENROWSET (BULK 'C:\JSON\Books\book.json', SINGLE_CLOB) as j
```

OPENJSON(BULK) 读取文件的内容并在 `BulkColumn` 中返回该内容。

你也可以加载文件的内容到本地变量或插入表中，如下面的示例中所示：

```sql
-- Load file contents into a variable
SELECT @json = BulkColumn
 FROM OPENROWSET (BULK 'C:\JSON\Books\book.json', SINGLE_CLOB) as j

-- Load file contents into a table 
SELECT BulkColumn
 INTO #temp 
 FROM OPENROWSET (BULK 'C:\JSON\Books\book.json', SINGLE_CLOB) as j
```

在加载 JSON 文件的内容之后, 你可以在表中保存 JSON 文本。

## <a name="import-multiple-json-documents"></a>导入多个 JSON 文档
可以使用相同的方法将一组的 JSON 文件从文件系统加载到一个本地变量一次。 假设这些文件命名为 `book<index>.json`。
  
```sql
DECLARE @i INT = 1
DECLARE @json AS NVARCHAR(MAX)

WHILE(@i < 10)
BEGIN
    SET @file = 'C:\JSON\Books\book' + cast(@i AS VARCHAR(5)) + '.json';
    SELECT @json = BulkColumn FROM OPENROWSET (BULK (@file), SINGLE_CLOB) AS j
    SELECT * FROM OPENJSON(@json) AS json
    -- Optionally, save the JSON text in a table.
    SET @i = @i + 1 ;
END
```

## <a name="import-json-documents-from-azure-file-storage"></a>从 Azure 文件存储导入 JSON 文档
你还可用于 openrowset （bulk） 上文所述从 SQL Server 可以访问其他文件位置读取 JSON 文件。 例如，Azure 文件存储支持 SMB 协议。 因此，你可以使用以下过程将本地虚拟驱动器映射到 Azure 文件存储共享：
1.  使用 Azure 门户或 Azure PowerShell 在 Azure 文件存储中创建一个文件存储帐户（例如 `mystorage`）、一个文件共享（例如 `sharejson`）和一个文件夹。
2.  将一些 JSON 文件上载到文件存储共享。
3.  在计算机上的 Windows 防火墙中创建一个允许端口 445 的出站防火墙规则。 请注意，Internet 服务提供商可能会阻止此端口。 如果以下步骤出现 DNS 错误（错误 53），则表示尚未打开端口 445，或者 ISP 阻止了该端口。
4. 装载 Azure 文件存储共享中的以本地驱动器 (例如`T:`)。

    以下是命令语法：

    ```
    net use [drive letter] \\[storage name].file.core.windows.net\[share name] /u:[storage account name] [storage account access key]
    ```

    下面是示例分配本地驱动器号`T:`到 Azure 文件存储共享：

    ```
    net use t: \\mystorage.file.core.windows.net\sharejson /u:myaccount hb5qy6eXLqIdBj0LvGMHdrTiygkjhHDvWjUZg3Gu7bubKLg==
    ```

    可以在 Azure 门户上“设置”对话框的“密钥”部分中找到存储帐户密钥以及主要或辅助存储帐户访问密钥。

5.  现在你可以访问 JSON 文件从 Azure 文件存储共享使用映射的驱动器中，如以下示例所示：

    ```sql
    SELECT book.* FROM
     OPENROWSET(BULK N't:\books\books.json', SINGLE_CLOB) AS json
     CROSS APPLY OPENJSON(BulkColumn)
     WITH( id nvarchar(100), name nvarchar(100), price float,
        pages_i int, author nvarchar(100)) AS book
    ```

有关 Azure 文件存储的详细信息，请参阅[文件存储](https://azure.microsoft.com/en-us/services/storage/files/)。

## <a name="import-json-documents-from-azure-blob-storage"></a>从 Azure Blob 存储导入 JSON 文档

使用 T-SQL 的大容量插入命令或 OPENROWSET 函数，可以直接在 Azure SQL 数据库从 Azure Blob 存储加载文件。

首先，创建外部数据源，如下面的示例中所示。

```sql
CREATE EXTERNAL DATA SOURCE MyAzureBlobStorage
 WITH ( TYPE = BLOB_STORAGE,
        LOCATION = 'https://myazureblobstorage.blob.core.windows.net',
        CREDENTIAL= MyAzureBlobStorageCredential);
```

接下来，结合 DATA_SOURCE 选项运行 BULK INSERT 命令。

```sql
BULK INSERT Product
FROM 'data/product.dat'
WITH ( DATA_SOURCE = 'MyAzureBlobStorage');
```

有关详细信息和使用 OPENROWSET 的示例，请参阅[文件从 Azure Blob 存储加载到 Azure SQL 数据库](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2017/02/23/loading-files-from-azure-blob-storage-into-azure-sql-database/)。

## <a name="parse-json-documents-into-rows-and-columns"></a>在行和列中分析 JSON 文档
而不是读取整个 JSON 文件作为单个值，你可能想要分析它，并返回丛书中的文件和行和列及其属性。 下面的示例使用从 JSON 文件[此站点](https://github.com/tamingtext/book/blob/master/apache-solr/example/exampledocs/books.json)包含的书籍的列表。

### <a name="example-1"></a>示例 1
在最简单的示例中，可以只从文件中加载整个列表。 

```sql
SELECT value
 FROM OPENROWSET (BULK 'C:\JSON\Books\books.json', SINGLE_CLOB) as j
 CROSS APPLY OPENJSON(BulkColumn)
```

### <a name="example-2"></a>示例 2
OPENROWSET 从文件中读取单个文本值，以 BulkColumn 的形式返回该值，并将其传递给 OPENJSON 函数。 OPENJSON 循环访问 BulkColumn 数组中的 JSON 对象的数组，并在每个行中，采用 JSON 格式返回一本书：

```
{"id":"978-0641723445″, "cat":["book","hardcover"], "name":"The Lightning Thief", … 
{"id":"978-1423103349″, "cat":["book","paperback"], "name":"The Sea of Monsters", … 
{"id":"978-1857995879″, "cat":["book","paperback"], "name":"Sophie’s World : The Greek … 
{"id":"978-1933988177″, "cat":["book","paperback"], "name":"Lucene in Action, Second … 
```

### <a name="example-3"></a>示例 3
OPENJSON 函数可分析 JSON 内容，并将其转换为表或结果集。 下面的示例加载内容，分析加载的 JSON，然后以列的形式返回五个字段：

```sql
SELECT book.*
 FROM OPENROWSET (BULK 'C:\JSON\Books\books.json', SINGLE_CLOB) as j
 CROSS APPLY OPENJSON(BulkColumn)
 WITH( id nvarchar(100), name nvarchar(100), price float,
 pages_i int, author nvarchar(100)) AS book
```

在此示例中，OPENROWSET(BULK) 读取文件的内容，并使用定义的架构将该内容传递给 OPENJSON 函数，以便输出内容。 OPENJSON 使用列名匹配 JSON 对象中的属性。 例如，`price` 属性将以 `price` 列的形式返回，并转换为浮点数据类型。 结果如下：

|ID|名称|price|pages_i|作者
|---|---|---|---|---|
978-0641723445|The Lightning Thief|12.5|384|Rick Riordan| 
978-1423103349|The Sea of Monsters|6.49|304|Rick Riordan| 
978-1857995879|Sophie’s World : The Greek Philosophers|3.07|64|Jostein Gaarder| 
978-1933988177|Lucene in Action, Second Edition|30.5|475|Michael McCandless| 

现在，可将此表返回给用户，或者将数据载入另一个表。

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>了解有关内置 JSON 支持在 SQL Server 中的详细信息  
对于大量的特定解决方案，使用情况和建议，请参阅[博客文章有关内置 JSON 支持](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)在 SQL Server 和 Azure SQL Database: Microsoft 项目经理 Jovan Popovic 中。
  
## <a name="see-also"></a>另请参阅
[使用 OPENJSON 将 JSON 数据转换为行和列](../../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md)


