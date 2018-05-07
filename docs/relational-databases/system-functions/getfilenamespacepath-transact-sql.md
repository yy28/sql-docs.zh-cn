---
title: GetFileNamespacePath (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- GetFileNamespacePath
- GetFileNamespacePath_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- GetFileNamespacePath function
ms.assetid: b393ecef-baa8-4d05-a268-b2f309fce89a
caps.latest.revision: 16
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a31ca80ae50906f0789fdfef20fbf4fede9beea8
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="getfilenamespacepath-transact-sql"></a>GetFileNamespacePath (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  返回 FileTable 中文件或目录的 UNC 路径。  
  
## <a name="syntax"></a>语法  
  
```  
  
<column-name>.GetFileNamespacePath(is_full_path, @option)  
```  
  
## <a name="arguments"></a>参数  
 *column-name*  
 Varbinary （max） 列名称**file_stream** FileTable 中的列。  
  
 *列名称*值必须是有效的列名。 它不能是表达式，也不能是从其他数据类型的列转换或强制转换的值。  
  
 *is_full_path*  
 整数表达式，指定是返回相对路径还是绝对路径。 *is_full_path*可以具有以下值之一：  
  
|“值”|说明|  
|-----------|-----------------|  
|**0**|返回数据库级目录内的相对路径。<br /><br /> 此为默认值。|  
|**1**|返回以 `\\computer_name` 开头的完整 UNC 路径。|  
  
 *@option*  
 一个整数表达式，定义路径的服务器组件应如何进行格式化。 *@option* 可以具有以下值之一：  
  
|“值”|说明|  
|-----------|-----------------|  
|**0**|返回转换为 NetBIOS 格式的服务器名称，例如：<br /><br /> `\\SERVERNAME\MSSQLSERVER\MyDocumentDatabase`<br /><br /> 这是默认值。|  
|**1**|返回未经转换的服务器名称，例如：<br /><br /> `\\ServerName\MSSQLSERVER\MyDocumentDatabase`|  
|**2**|返回完整的服务器路径，例如：<br /><br /> `\\ServerName.MyDomain.com\MSSQLSERVER\MyDocumentDatabase`|  
  
## <a name="return-type"></a>返回类型  
 **nvarchar(max)**  
  
 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例属于故障转移群集系统，则作为此路径的一部分返回的计算机名称将是群集实例的虚拟主机名。  
  
 如果数据库属于 Alwayson 可用性组，则**FileTableRootPath**函数返回而不是计算机名称的虚拟网络名称 (VNN)。  
  
## <a name="general-remarks"></a>一般备注  
 路径的**GetFileNamespacePath**函数返回与以下格式的逻辑目录或文件路径：  
  
 `\\<machine>\<instance-level FILESTREAM share>\<database-level directory>\<FileTable directory>\...`  
  
 此逻辑路径不直接对应于某一物理 NTFS 路径。 FILESTREAM 的文件系统筛选器驱动程序和 FILESTREAM 代理会将该逻辑路径转换为物理路径。 逻辑路径和物理路径之间的这一区别使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以在内部重新组织数据并且不会影响路径的有效性。  
  
## <a name="best-practices"></a>最佳实践  
 若要使代码和应用程序独立于当前的计算机和数据库，应避免编写依赖于绝对文件路径的代码。 相反，获得的完整路径的文件在运行时通过使用**FileTableRootPath**和**GetFileNamespacePath**函数组合，如下面的示例中所示。 默认情况下， **GetFileNamespacePath** 函数返回数据库根路径下的文件的相对路径。  
  
```sql  
USE MyDocumentDatabase;  
@root varchar(100)  
SELECT @root = FileTableRootPath();  
  
@fullPath = varchar(1000);  
SELECT @fullPath = @root + file_stream.GetFileNamespacePath() FROM DocumentStore  
WHERE Name = N’document.docx’;  
```  
  
## <a name="remarks"></a>注释  
  
## <a name="examples"></a>示例  
 下面的示例演示如何调用**GetFileNamespacePath**函数可获取文件或目录在 FileTable 中的 UNC 路径。  
  
```  
-- returns the relative path of the form “\MyFileTable\MyDocDirectory\document.docx”  
SELECT file_stream.GetFileNamespacePath() AS FilePath FROM DocumentStore  
WHERE Name = N’document.docx’;  
  
-- returns “\\MyServer\MSSQLSERVER\MyDocumentDatabase\MyFileTable\MyDocDirectory\document.docx”  
SELECT file_stream.GetFileNamespacePath(1, Null) AS FilePath FROM DocumentStore  
WHERE Name = N’document.docx’;  
```  
  
## <a name="see-also"></a>另请参阅  
 [在 FileTable 中使用目录和路径](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)  
  
  
