---
title: ALTER EXTERNAL LIBRARY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/05/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER EXTERNAL LIBRARY
- ALTER_EXTERNAL_LIBRARY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER EXTERNAL LIBRARY
author: jeannt
ms.author: jeannt
manager: craigg
ms.openlocfilehash: e2fb628e2f832b7d1b73a2e3fefae1fb1d6b8e2b
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2018
---
# <a name="alter-external-library-transact-sql"></a>ALTER EXTERNAL LIBRARY (Transact-SQL)  

[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

修改现有外部包库的内容。

## <a name="syntax"></a>语法

```text
ALTER EXTERNAL LIBRARY library_name
[ AUTHORIZATION owner_name ]
SET <file_spec>
WITH ( LANGUAGE = 'R' )
[ ; ]

<file_spec> ::=
{
(CONTENT = { <client_library_specifier> | <library_bits> | NONE}
[, PLATFORM = WINDOWS )
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

指定现有包库的名称。 库的应用范围限定为用户。 在特定用户或所有者的上下文中，库名称必须是唯一的。

不能任意分配库名称。 也就是说，必须使用调用运行时在加载包时需要的名称。

**owner_name**

指定拥有外部库的用户或角色的名称。

**file_spec**

指定特定平台的包的内容。 每个平台仅支持一个文件项目。

可以是以本地路径或网络路径的形式指定的文件。 如果指定了数据源选项，则文件名称可以是关于 `EXTERNAL DATA SOURCE` 中引用的容器的相对路径。

还可以为文件指定一个 OS 平台。 针对特定语言或运行时，每个 OS 平台只允许一个文件项目或内容。

**library_bits**

将包的内容指定为十六进制文本，类似于程序集。 

如果具有更改库所需的权限，但在服务器上访问文件受到限制，并且无法将内容保存到服务器可以访问的路径，则此选项非常有用。

相反，可以将包内容作为变量以二进制格式进行传递。

**PLATFORM = WINDOWS**

为库的内容指定平台。 在修改现有库以添加不同的平台时，此值是必需的。 Windows 是唯一支持的平台。

## <a name="remarks"></a>Remarks

对于 R 语言，准备包时，包的形式须为适用于 Windows 、扩展名为 .ZIP 的压缩存档文件。 目前仅支持 Windows 平台。  

`ALTER EXTERNAL LIBRARY` 语句只将库位上载到数据库。 当用户在调用库的 [sp_execute_external_script (TRANSACT-SQL)](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 中运行代码时，安装已修改的库。

## <a name="permissions"></a>权限

默认情况下，dbo 用户或担任 db_owner 角色的任何成员都有权运行 ALTER EXTERNAL LIBRARY。 此外，创建了外部库的用户还可以更改相应外部库。

## <a name="examples"></a>示例

下面的示例更改 `customPackage` 外部库。

### <a name="a-replace-the-contents-of-a-library-using-a-file"></a>A. 使用文件替换库的内容

下面的示例使用包含更新位的压缩文件修改名为 `customPackage` 的外部库。

```sql
ALTER EXTERNAL LIBRARY customPackage 
SET 
  (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\customPackage.zip')
WITH (LANGUAGE = 'R');
```

若要安装更新的库，请执行存储过程 `sp_execute_external_script`。

```sql
EXEC sp_execute_external_script 
@language =N'R', 
@script=N'library(customPackage)'
;
```

### <a name="b-alter-an-existing-library-using-a-byte-stream"></a>B. 使用字节流更改现有库

下面的示例通过将新位传递为十六进制文本来更改现有库。

```SQL
ALTER EXTERNAL LIBRARY customLibrary 
SET (CONTENT = 0xabc123) WITH (LANGUAGE = 'R');
```

> [!NOTE]
> 此代码示例只用于展示语法；为了提高可读性，`CONTENT =` 中的二进制值已遭截断，无法创建能够正常运行的库。 二进制变量的实际内容要长得多。

## <a name="see-also"></a>另请参阅

[CREATE EXTERNAL LIBRARY (Transact-SQL)](create-external-library-transact-sql.md)
[DROP EXTERNAL LIBRARY (Transact-SQL)](drop-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md) 
