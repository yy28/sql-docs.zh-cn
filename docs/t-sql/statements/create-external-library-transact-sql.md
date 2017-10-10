---
title: "创建外部库 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 10/05/2017
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
ms.sourcegitcommit: 29122bdf543e82c1f429cf401b5fe1d8383515fc
ms.openlocfilehash: 8066d267790f346a22a649fb0c873a3d454489a8
ms.contentlocale: zh-cn
ms.lasthandoff: 10/10/2017

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

**library_bits**

为十六进制文字，类似于程序集指定包的内容。 此选项允许用户创建一个要更改库，如果它们有所要求的权限，但不是能文件路径访问服务器可访问的任何文件夹的库。

**平台 = WINDOWS**

指定内容库的平台。 值默认为在其运行 SQL Server 的主机平台。 因此，用户不具有指定值。 它是必需的以防其中支持多个平台，或用户需要指定一个不同的平台。 Windows 是唯一受支持的平台。

## <a name="remarks"></a>注释

对于 R 语言中，使用的文件时，包必须准备与压缩的存档文件的形式。适用于 Windows 的 ZIP 扩展。 目前，支持仅 Windows 平台

`CREATE EXTERNAL LIBRARY`语句仅将库 bits 上载到数据库。 库未实际安装用户运行的外部脚本之后，通过执行之前[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。  

库上载到该实例可以是公共或私有。 如果库创建的成员`dbo`，该库是公共的并可以与所有用户共享。 否则，为专用于该用户仅库。

SQL Server 2017 版本中的数据源中不能用作 blob。

## <a name="permissions"></a>Permissions

需要`CREATE ANY EXTERNAL LIBRARY`权限。

若要修改的库，需要单独的权限， `ALTER ANY EXTERNAL LIBRARY`。

## <a name="examples"></a>示例

### <a name="a-add-an-external-library-to-a-database"></a>A. 向数据库添加外部库  

下面的示例添加外部库调用 customPackage 到数据库。

```sql
CREATE EXTERNAL LIBRARY customPackage 
FROM 
  (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\customPackage.zip')
WITH (LANGUAGE = 'R');
```  

库已成功上载到的实例后，用户执行`sp_execute_external_script`过程中，若要安装的库。

```sql
EXEC sp_execute_external_script 
@language =N'R', 
@script=N'
# load customPackage
library(customPackage)
'
```

### <a name="b-installing-packages-with-dependencies"></a>B. 具有依赖项安装包

如果`packageB`具有依赖关系`packageA`，然后按照这些一般原则：

+ 上载目标包和其依赖项。

    这两个包必须是服务器可访问的文件夹中。

    ```sql
    CREATE EXTERNAL LIBRARY packageA 
    FROM (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\packageA.zip') 
    WITH (LANGUAGE = 'R'); 
    
    CREATE EXTERNAL LIBRARY packageB FROM (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\packageB.zip') 
    WITH (LANGUAGE = 'R');
    ```

+ 首先安装依赖关系。

    如果所需的程序包`packageA`已上载到的实例，它需要不具有已单独安装。 所需的程序包`packageA`将时安装`sp_execute_external_script`首次运行以安装包`packageB`。

    但是，如果所需的程序包， `packageA`，不可用，安装目标包`packageB`将失败。

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

### <a name="c-create-a-library-from-a-byte-stream"></a>C. 从字节流中创建库

下面的示例创建一个库，通过传递作为十六进制文本更新 bits。

```SQL
CREATE EXTERNAL LIBRARY customLibrary FROM (CONTENT = 0xabc123) WITH (LANGUAGE = 'R');
```

### <a name="d-change-an-existing-package-library"></a>D. 更改现有包库

`ALTER EXTERNAL LIBRARY` DDL 语句可用于添加新库内容或修改现有库内容。 若要修改的现有库需要`ALTER ANY EXTERNAL LIBRARY`权限。

有关详细信息，请参阅[ALTER 外部库](alter-external-library-transact-sql.md)。

### <a name="e-delete-a-package-library"></a>E. 删除包库

要从数据库中删除包库，请运行语句：

```sql
DROP EXTERNAL LIBRARY customPackage <user_name>;
```

> [!NOTE]
> 与其他不同`DROP`中的语句[!INCLUDE[ssnoversion](../../includes/ssnoversion.md)]，此语句支持可选参数，指定了用户的权限。 此选项允许具有所有权角色的用户删除由常规用户上载的库。

## <a name="see-also"></a>另请参阅

[ALTER 外部库 (Transact SQL)](alter-external-library-transact-sql.md)  
[删除外部库 (Transact SQL)](drop-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)  

