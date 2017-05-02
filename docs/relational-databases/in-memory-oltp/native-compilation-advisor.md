---
title: "本机编译顾问 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.nativecompilationwizard.f1
- swb.nativecompilationwizard.f1
ms.assetid: d3898a47-2985-4a08-bc70-fd8331a01b7b
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6a6107fe8c3b05c31320f90c77df04731e226ba8
ms.lasthandoff: 04/11/2017

---
# <a name="native-compilation-advisor"></a>本机编译顾问
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  借助事务性能分析报告，你可以了解数据库中的哪些已解释的存储过程在移植后使用本机编译会给你带来好处。 有关详细信息，请参阅 [确定表或存储过程是否应移植到内存中 OLTP](../../relational-databases/in-memory-oltp/determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md)。  
  
 确定要在移植后使用本机编译的存储过程后，你可以使用本机编译顾问 (NCA) 来帮助你将已解释的存储过程迁移到本地编译。 有关本机编译的存储过程的详细信息，请参阅 [Natively Compiled Stored Procedures](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)。  
  
 在给定的已解释的存储过程中，NCA 可方便你确定本机模块不支持的所有功能。 NCA 提供解决方法或解决方案的文档链接。  
  
 有关迁移方法的信息，请参阅 [内存中 OLTP - 常见的工作负荷模式和迁移注意事项](http://msdn.microsoft.com/library/dn673538.aspx)。  
  
## <a name="walkthrough-using-the-native-compilation-advisor"></a>使用本机编译顾问的演练  
 在 **对象资源管理器**中，右键单击要转换的存储过程，然后选择 **“本机编译顾问”**。 这将显示 **“存储过程本机编译顾问”**的欢迎使用页。 单击 **“下一步”** 继续。  
  
### <a name="stored-procedure-validation"></a>存储过程验证  
 此页将报告存储过程是否使用与本机编译不兼容的任何构造。 您可以单击 **“下一步”** 查看详细信息。 如果存在与本机编译不兼容的构造，可以单击 **“下一步”** 查看详细信息。  
  
### <a name="stored-procedure-validation-result"></a>存储过程验证结果  
 如果存在与本机编译不兼容的构造，则 **“存储过程验证结果”** 页将显示详细信息。 你可以生成报表（单击“生成报表”****）、退出“本机编译顾问”****以及更新你的代码以便它与本机编译兼容。  
  
## <a name="code-sample"></a>代码示例  
 下面的示例展示了已解释的存储过程，以及适用于本机编译的 *等效* 存储过程。 该示例假定名为 c:\data 的目录。  
  
> [!NOTE]  
>  和往常一样， **FILEGROUP** 元素和 **USE** mydatabase 语句可应用于 Microsoft SQL Server，但不可应用于 Azure SQL 数据库。  
  
```tsql  
CREATE DATABASE Demo  
ON  
PRIMARY(NAME = [Demo_data],  
FILENAME = 'C:\DATA\Demo_data.mdf', size=500MB)  
, FILEGROUP [Demo_fg] CONTAINS MEMORY_OPTIMIZED_DATA(  
NAME = [Demo_dir],  
FILENAME = 'C:\DATA\Demo_dir')  
LOG ON (name = [Demo_log], Filename='C:\DATA\Demo_log.ldf', size=500MB)  
COLLATE Latin1_General_100_BIN2;  
go  
  
USE Demo;  
go  
  
CREATE TABLE [dbo].[SalesOrders]  
(  
     [order_id] [int] NOT NULL,  
     [order_date] [datetime] NOT NULL,  
     [order_status] [tinyint] NOT NULL  
     CONSTRAINT [PK_SalesOrders] PRIMARY KEY NONCLUSTERED HASH   
(  
     [order_id]  
) WITH ( BUCKET_COUNT = 2097152)  
) WITH ( MEMORY_OPTIMIZED = ON )  
go  
  
-- Interpreted.  
CREATE PROCEDURE [dbo].[InsertOrder] @id INT, @date DATETIME2, @status TINYINT  
AS   
BEGIN   
  INSERT dbo.SalesOrders VALUES (@id, @date, @status);  
END  
go  
  
-- Natively Compiled.  
CREATE PROCEDURE [dbo].[InsertOrderXTP]  
      @id INT, @date DATETIME2, @status TINYINT  
  WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS   
BEGIN ATOMIC WITH   
     (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english'  
     )  
  INSERT dbo.SalesOrders VALUES (@id, @date, @status);  
END  
go  
  
SELECT * from SalesOrders;  
go  
  
EXECUTE dbo.InsertOrder @id= 10, @date = '1956-01-01 12:00:00', @status = 1;  
EXECUTE dbo.InsertOrderXTP @id= 11, @date = '1956-01-01 12:01:00', @status = 2;  
  
SELECT * from SalesOrders;  
```  
  
## <a name="see-also"></a>另请参阅  
 [迁移到内存中 OLTP](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)   
 [使用内存优化表的要求](../../relational-databases/in-memory-oltp/requirements-for-using-memory-optimized-tables.md)  
  
  
