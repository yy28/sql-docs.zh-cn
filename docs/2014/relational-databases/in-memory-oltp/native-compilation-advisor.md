---
title: 本机编译顾问 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
f1_keywords:
- sql12.swb.nativecompilationwizard.f1
- swb.nativecompilationwizard.f1
ms.assetid: d3898a47-2985-4a08-bc70-fd8331a01b7b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 36a6a30ffbf5a0991e2b55ba655549454516e82d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48147097"
---
# <a name="native-compilation-advisor"></a>本机编译顾问
  事务性能报告工具 (请参阅[确定表或存储过程应移植到内存中 OLTP 是否](determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md)) 会通知你哪些解释型存储的过程在数据库中受益如果移植到使用本机编译。 在您标识要移植到使用本机编译的存储过程后，可以使用本机编译顾问来帮助您将已解释的存储过程迁移到本地编译。 有关本机编译的存储过程的详细信息，请参阅 [Natively Compiled Stored Procedures](natively-compiled-stored-procedures.md)。  
  
 开始时，连接至包含已解释的存储过程的实例。 您可以连接到 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 或 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 实例。 但是，如果您想要使用该顾问执行迁移操作，则必须连接到启用了内存中 OLTP 功能的 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 实例。 有关内存中 OLTP 要求的详细信息，请参阅 [Requirements for Using Memory-Optimized Tables](memory-optimized-tables.md)。  
  
 有关迁移方法的信息，请参阅 [内存中 OLTP - 常见的工作负荷模式和迁移注意事项](http://msdn.microsoft.com/library/dn673538.aspx)。  
  
## <a name="walkthrough-using-the-native-compilation-advisor"></a>使用本机编译顾问的演练  
 在 **对象资源管理器**中，右键单击要转换的存储过程，然后选择 **“本机编译顾问”**。 这将显示 **“存储过程本机编译顾问”** 的欢迎使用页。 单击 **“下一步”** 继续。  
  
### <a name="stored-procedure-validation"></a>存储过程验证  
 此页将报告存储过程是否使用与本机编译不兼容的任何构造。 您可以单击 **“下一步”** 查看详细信息。 如果存在与本机编译不兼容的构造，可以单击 **“下一步”** 查看详细信息。  
  
### <a name="stored-procedure-validation-result"></a>存储过程验证结果  
 如果存在与本机编译不兼容的构造，则 **“存储过程验证结果”** 页将显示详细信息。 你可以生成报表（单击“生成报表”）、退出“本机编译顾问”以及更新你的代码以便它与本机编译兼容。  
  
## <a name="code-sample"></a>代码示例  
 下面的示例显示了一个已解释的存储过程以及针对本机编译的等效存储过程。 该示例假定名为 c:\data 的目录。  
  
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
GO  
USE Demo;  
GO  
  
CREATE TABLE [dbo].[SalesOrders]  
(  
     [order_id] [int] NOT NULL,  
     [order_date] [datetime] NOT NULL,  
     [order_status] [tinyint] NOT NULL  
  
CONSTRAINT [PK_SalesOrders] PRIMARY KEY NONCLUSTERED HASH   
(  
     [order_id]  
)WITH ( BUCKET_COUNT = 2097152)  
)WITH ( MEMORY_OPTIMIZED = ON )  
  
go  
  
CREATE PROCEDURE [dbo].[InsertOrder] @id INT, @date DATETIME2, @status TINYINT  
AS   
BEGIN   
  
  INSERT dbo.SalesOrders VALUES (@id, @date, @status)  
  
END  
  
go  
  
CREATE PROCEDURE [dbo].[InsertOrderXTP] @id INT, @date DATETIME2, @status TINYINT  
  WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS   
BEGIN ATOMIC WITH   
(    TRANSACTION ISOLATION LEVEL = SNAPSHOT,  
     LANGUAGE = N'us_english')  
  
  INSERT dbo.SalesOrders VALUES (@id, @date, @status)  
  
END  
go  
  
select * from SalesOrders  
go  
exec dbo.InsertOrder @id= 10, @date = '1956-01-01 12:00:00', @status = 1 ;  
exec dbo.InsertOrderXTP @id= 11, @date = '1956-01-01 12:01:00', @status = 2 ;  
select * from SalesOrders  
```  
  
## <a name="see-also"></a>请参阅  
 [迁移到内存中 OLTP](migrating-to-in-memory-oltp.md)  
  
  
