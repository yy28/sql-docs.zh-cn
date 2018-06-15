---
title: FileTableRootPath (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- FileTableRootPath_TSQL
- FileTableRootPath
dev_langs:
- TSQL
helpviewer_keywords:
- FileTableRootPath function
ms.assetid: 0cba908a-c85c-4b09-b16a-df1cb333c629
caps.latest.revision: 15
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 637653dc75154f00c14cb248703aec3645f313bb
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33230507"
---
# <a name="filetablerootpath-transact-sql"></a>FileTableRootPath (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  返回特定 FileTable 或当前数据库的根级 UNC 路径。  
  
## <a name="syntax"></a>语法  
  
```  
  
FileTableRootPath ( [ ‘[schema_name.]FileTable_name’ ], @option )  
```  
  
## <a name="arguments"></a>参数  
 *FileTable_name*  
 FileTable 的名称。 *FileTable_name*属于类型**nvarchar**。 这是一个可选参数。 默认值为当前数据库。 指定*schema_name*也是可选的。 您可以传递 NULL *FileTable_name*若要使用的默认参数值  
  
 *@option*  
 一个整数表达式，定义路径的服务器组件应如何进行格式化。 *@option* 可以具有以下值之一：  
  
|“值”|说明|  
|-----------|-----------------|  
|**0**|返回转换为 NetBIOS 格式的服务器名称，例如：<br /><br /> `\\SERVERNAME\MSSQLSERVER\MyDocumentDatabase`<br /><br /> 这是默认值。|  
|**1**|返回未经转换的服务器名称，例如：<br /><br /> `\\ServerName\MSSQLSERVER\MyDocumentDatabase`|  
|**2**|返回完整的服务器路径，例如：<br /><br /> `\\ServerName.MyDomain.com\MSSQLSERVER\MyDocumentDatabase`|  
  
## <a name="return-type"></a>返回类型  
 **nvarchar(4000)**  
  
 如果数据库属于 Alwayson 可用性组，则**FileTableRootPath**函数返回而不是计算机名称的虚拟网络名称 (VNN)。  
  
## <a name="general-remarks"></a>一般备注  
 **FileTableRootPath**当满足以下条件之一时，函数将返回 NULL:  
  
-   值*FileTable_name*无效。  
  
-   调用方没有足够的权限引用指定表或当前数据库。  
  
-   FILESTREAM 选项的*database_directory*没有为当前数据库设置。  
  
 有关详细信息，请参阅 [Work with Directories and Paths in FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)。  
  
## <a name="best-practices"></a>最佳实践  
 若要使代码和应用程序独立于当前的计算机和数据库，应避免编写依赖于绝对文件路径的代码。 相反，获得的完整路径的文件在运行时通过使用**FileTableRootPath**和**GetFileNamespacePath**函数组合，如下面的示例中所示。 默认情况下， **GetFileNamespacePath** 函数返回数据库根路径下的文件的相对路径。  
  
```sql  
USE MyDocumentDatabase;  
  
@root varchar(100)  
SELECT @root = FileTableRootPath();  
@fullPath = varchar(1000);  
  
SELECT @fullPath = @root + file_stream.GetFileNamespacePath()  
FROM DocumentStore  
WHERE Name = N’document.docx’;  
```  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>权限  
 **FileTableRootPath**函数需要：  
  
-   拥有 FileTable 的 SELECT 权限以获取特定 FileTable 的根路径。  
  
-   **db_datareader**或更高的根路径获取当前数据库的权限。  
  
## <a name="examples"></a>示例  
 下面的示例演示如何调用**FileTableRootPath**函数。  
  
```  
USE MyDocumentDatabase;  
-- returns “\\MYSERVER\MSSQLSERVER\MyDocumentDatabase”  
SELECT FileTableRootPath();  
  
-- returns “\\MYSERVER\MSSQLSERVER\MyDocumentDatabase\MyFileTable”  
SELECT FileTableRootPath(N'dbo.MyFileTable');  
  
-- returns “\\MYSERVER\MSSQLSERVER\MyDocumentDatabase\MyFileTable”  
SELECT FileTableRootPath(N'MyFileTable');  
```  
  
## <a name="see-also"></a>另请参阅  
 [在 FileTable 中使用目录和路径](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)  
  
  
