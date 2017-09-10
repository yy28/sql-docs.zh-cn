---
title: "创建外部库 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/18/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE EXTERNAL LIBRARY
- CREATE_EXTERNAL_LIBRARY_TSQL
- EXTERNAL LIBRARY
- EXTERNAL_LIBRARY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE EXTERNAL LIBRARY
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0f11a6b7633be392e1f789e12c43f2e5d6e56b47
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="create-external-library-transact-sql"></a>创建外部库 (Transact SQL)  
[!INCLUDE[tsql-appliesto-ssvnxt-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]  

将 R 包上载到数据库中，从指定的字节流或文件路径。

此语句作为泛型机制的数据库管理员可以上载所需的任何新外部语言运行时 （R、 Python、 Java 等） 的项目和支持的操作系统平台[!INCLUDE[ssnoversion](../../includes/ssnoversion.md)]。 目前仅将 R 语言和 Windows 平台支持。

## <a name="syntax"></a>语法

```
CREATE EXTERNAL LIBRARY library_name  
    [ AUTHORIZATION owner_name ]  
FROM <file_spec> [,…2]  
WITH ( LANGUAGE = 'R' )  
[ ; ]  

<file_spec> ::=  
{  
(CONTENT = { <client_library_specifier> | <library_bits> }  
[, PLATFORM = WINDOWS ])  
}  

<client_library_specifier> :: =  
  '[\\computer_name\]share_name\[path\]manifest_file_name'  
| '[local_path\]manifest_file_name'  
| '<relative_path_in_external_data_source>'  

<library_bits> :: =  
{ varbinary_literal | varbinary_expression }  
```

### <a name="arguments"></a>参数

**library_name**

库将添加到作用域为用户数据库。 也就是说，库名称被视为特定用户或所有者的上下文中的唯一和库名称必须是唯一每个用户。 例如，两个用户**RUser1**和**RUser2**可以同时单独和单独上载 R 库`ggplot2`。 

**owner_name**

指定用户或角色拥有外部库的名称。 如果未指定，则所有权授予当前用户。

拥有的数据库所有者的库都被视为全局到数据库和运行时。 换而言之，数据库所有者可以创建包含一组通用的库或多个用户共享的包的库。 外部库创建时由用户以外`dbo`用户，外部库是私有的只有该用户。   

当用户**RUser1**执行 R 脚本，值`libPath`可以包含多个路径。 第一个路径始终是由数据库所有者创建的共享库的路径。 第二部分`libPath`指定包含单独通过上载的包的路径**RUser1**。

**file_spec**

指定特定平台的包的内容。 支持每个平台的一个文件项目。 

可以在本地路径或网络路径的形式指定的文件。

（可选） 可以指定一个操作系统平台，该文件。 只有一个文件项目或内容被为了针对特定语言或运行每个操作系统平台。

**平台 = WINDOWS**

指定内容库的平台。 值默认为在其运行 SQL Server 的主机平台。 因此，用户不具有指定值。 它是必需的以防其中支持多个平台，或用户需要指定一个不同的平台。 Windows 是唯一受支持的平台。

## <a name="remarks"></a>注释

对于 R 语言中，包必须准备与压缩的存档文件的形式。适用于 Windows 的 ZIP 扩展。 目前，支持仅 Windows 平台。  

`CREATE EXTERNAL LIBRARY`语句仅将库 bits 上载到数据库。 库未实际安装用户运行的外部脚本之后，通过执行之前[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。  

## <a name="permissions"></a>Permissions  
需要`CREATE EXTERNAL LIBRARY`权限。  

## <a name="examples"></a>示例

### <a name="a-add-an-external-library-to-a-database"></a>A. 向数据库添加外部库  
下面的示例添加外部库调用 customPackage 到数据库。   
```sql
CREATE EXTERNAL LIBRARY customPackage 
FROM 
  (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\customPackage.zip')
WITH (LANGUAGE = 'R');
```  
然后执行`sp_execute_external_script`过程中，若要安装的库。  
```sql
EXEC sp_execute_external_script 
@language =N'R', 
@script=N'
# load customPackage
library(customPackage)

# call customPackageFunc
OutputDataSet <- customPackageFunc()
'
with result sets (([result] int));    
```

### <a name="b-installing-packages-with-dependencies"></a>B. 具有依赖项安装包

如果`packageB`具有依赖关系`packageA`，然后代码例如遵循这些常规主体：   
```
CREATE EXTERNAL LIBRARY packageA 
FROM 
  (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\ggplot2.zip') 
WITH (LANGUAGE = 'R'); 

CREATE EXTERNAL LIBRARY packageB FROM 
  (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\ggplot2.zip') 
WITH (LANGUAGE = 'R');
```

`packageA`和`packageB`是否同时安装时`sp_execute_external_script`首次运行。   
```sql
EXEC sp_execute_external_script 
@language =N'R', 
@script=N'
# load packageB
library(packageB)

# call customPackageBFunc
OutputDataSet <- customPackageBFunc()
'
with result sets (([result] int));    
```

对于这种方式，保存包的文件夹必须是服务器可访问。 

### <a name="change-an-existing-package-library"></a>更改现有包库

`ALTER EXTERNAL LIBRARY` DDL 语句可用于添加新库内容或修改现有库内容。   

### <a name="delete-a-package-library"></a>删除包库

要从数据库中删除包库，请运行语句：

```sql
DROP EXTERNAL LIBRARY ggplot2 <user_name>;
```

> [!NOTE]
> 与其他不同`DROP`中的语句[!INCLUDE[ssnoversion](../../includes/ssnoversion.md)]，此语句支持可选参数，指定了用户的权限。 此选项允许具有所有权角色的用户删除由常规用户上载的库。 

## <a name="see-also"></a>另请参阅  
[ALTER 外部库 (Transact SQL)](alter-external-library-transact-sql.md)  
[删除外部库 (Transact SQL)](drop-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)  

