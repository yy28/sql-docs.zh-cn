---
title: "Create Table SQL 语句 （SQL Server 导入和导出向导） |Microsoft 文档"
ms.custom: 
ms.date: 02/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.createtablesql.f1
ms.assetid: 0d6f6b3b-d023-4770-a8a9-65b2977c8d05
caps.latest.revision: 67
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ad9b68e2a0ac4cd88917a7b45c7a8f12b14f3ab4
ms.contentlocale: zh-cn
ms.lasthandoff: 09/26/2017

---
# <a name="create-table-sql-statement-sql-server-import-and-export-wizard"></a>Create Table SQL 语句（SQL Server 导入和导出向导）
在“列映射”  对话框中，如果选择“创建目标表”  ，然后选择“编辑 SQL”  ，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导会显示“Create Table SQL 语句”  对话框。 在此页上，可查看并根据需要自定义 **CREATE TABLE** 命令，向导会运行该命令以创建新的目标表。
  
> [!NOTE]
> 如果在查找有关 [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE TABLE 语句的信息，而不是有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导的“Create Table SQL 语句”对话框的信息，请参阅 [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)。 
  
## <a name="screen-shot-of-the-create-table-sql-statement-page"></a>“Create Table SQL 语句”页面的屏幕截图  
 以下屏幕截图显示向导的“Create Table SQL 语句”  对话框。
 
在此示例中，“SQL 语句”  框包含由向导生成的默认 **CREATE TABLE** 语句。 此语句将创建名为的新目标表**Person.AddressNew**是一份**Person.Address**源表。 
  
 ![导入和导出向导创建表页](../../integration-services/import-export-data/media/create-table.png "导入和导出向导创建表页")  
  
## <a name="review-or-regenerate-the-create-table-statement"></a>查看或重新生成 CREATE TABLE 语句  
 **SQL 语句**  
显示自动生成的 SQL 语句，允许对其进行自定义。
 
如果更改默认 CREATE TABLE 命令时，可能需要对关联的列映射进行更改，当您返回到**列映射**对话框。  
  
若要在 SQL 语句的文本中包括回车符，请按 Ctrl+Enter。 如果只按 Enter，则对话框将关闭。  
  
有关 CREATE TABLE 语句和语法的详细信息，请参阅 [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)。   
  
 **自动生成**  
 还原默认的 SQL 语句，如果你已更改，通过单击**自动生成**。  
  
## <a name="create-a-table-that-includes-a-filestream-column"></a>创建包含 FILESTREAM 列的表  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 导入和导出向导会基于所连接的数据源生成默认 CREATE TABLE 语句。 即使源表具有 FILESTREAM 列，此默认 CREATE TABLE 语句也不会包含 FILESTREAM 属性。
 1.  若要使用向导复制 FILESTREAM 列，请首先在目标数据库上实现 FILESTREAM 存储。
 2.  然后在“Create Table SQL 语句”  对话框中将 FILESTREAM 属性手动添加到 CREATE TABLE 语句中。  

有关语法的详细信息，请参阅[CREATE TABLE &#40;Transact SQL &#41;](../../t-sql/statements/create-table-transact-sql.md). 有关 FILESTREAM 的详细信息，请参阅[二进制大型对象 (Blob) 数据 (SQL Server)](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)。  
  
## <a name="whats-next"></a>下一步是什么？  
 查看并自定义 CREATE TABLE 命令，然后单击“确定” 之后，“Create Table SQL 语句”  对话框会使你返回到“列映射”  对话框。 有关详细信息，请参阅 [列映射](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md)。
 
 ## <a name="see-also"></a>另请参阅
[导入和导出向导的简单示例入门](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)



