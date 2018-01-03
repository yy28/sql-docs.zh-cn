---
title: "ALTER 外部库 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 10/05/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER EXTERNAL LIBRARY
- ALTER_EXTERNAL_LIBRARY_TSQL
dev_langs: TSQL
helpviewer_keywords: ALTER EXTERNAL LIBRARY
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: 28a62f00b479506e919faf2cbdbf1202045192eb
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="alter-external-library-transact-sql"></a>ALTER 外部库 (Transact SQL)  

[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

修改现有的外部包库的内容。

## <a name="syntax"></a>语法

```
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

指定现有的包库的名称。 库的应用范围限定为用户。 也就是说，库名称被视为在特定用户或所有者的上下文中是唯一。

**owner_name**

指定用户或角色拥有外部库的名称。

**file_spec**

指定特定平台的包的内容。 支持每个平台的一个文件项目。

可以是本地路径或网络路径的形式指定的文件。 如果指定的数据源选项，则文件名称可以是与容器中引用的相对路径`EXTERNAL DATA SOURCE`。

（可选） 可以指定一个操作系统平台，该文件。 只有一个文件项目或内容被为了针对特定语言或运行每个操作系统平台。

**DATA_SOURCE = external_data_source_name**

指定包含库文件的位置的外部数据源的名称。 此位置应引用 Azure blob 存储路径。 若要创建外部数据源，使用[CREATE EXTERNAL DATA SOURCE (TRANSACT-SQL)](create-external-data-source-transact-sql.md)。

> [!IMPORTANT] 
> 目前，blob 不支持为 SQL Server 2017 版本中的数据源中。

**library_bits**

为十六进制文字，类似于程序集指定包的内容。 此选项允许用户创建一个要更改库，如果它们有所要求的权限，但不是能文件路径访问服务器可访问的任何文件夹的库。

**平台 = WINDOWS**

指定内容库的平台。 修改现有的库来添加不同的平台时，此值是必需的。 Windows 是唯一受支持的平台。

## <a name="remarks"></a>Remarks

对于 R 语言中，包必须准备与压缩的存档文件的形式。适用于 Windows 的 ZIP 扩展。 目前，支持仅 Windows 平台。  

`ALTER EXTERNAL LIBRARY`语句仅将库 bits 上载到数据库。 已修改的库用户运行的外部脚本之后，通过执行之前未实际安装[sp_execute_external_script (TRANSACT-SQL)](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。

## <a name="permissions"></a>权限

需要`ALTER ANY EXTERNAL LIBRARY`权限。 创建外部库，用户可以更改该外部的库。

## <a name="examples"></a>示例

下面的示例修改了名为 customPackage 外部库。

### <a name="a-replace-the-contents-of-a-library-using-a-file"></a>A. 使用文件的库的内容替换

下面的示例修改外部库调用 customPackage，使用包含的更新的位的压缩的文件。

```sql
ALTER EXTERNAL LIBRARY customPackage 
SET 
  (CONTENT = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\customPackage.zip')
WITH (LANGUAGE = 'R');
```  

若要安装更新的库，请执行存储的过程`sp_execute_external_script`。

```sql   
EXEC sp_execute_external_script 
@language =N'R', 
@script=N'
# load customPackage
library(customPackage)
# call customPackageFunc
OutputDataSet <- customPackageFunc()
'
WITH RESULT SETS (([result] int));
```

### <a name="b-alter-an-existing-library-using-a-byte-stream"></a>B. Alter 使用字节流的现有库

下面的示例通过将新的 bits 传递为十六进制文本更改现有的库。

```SQL
ALTER EXTERNAL LIBRARY customLibrary FROM (CONTENT = 0xabc123) WITH (LANGUAGE = 'R');
```

## <a name="see-also"></a>另请参阅  

[创建外部库 (Transact SQL)](create-external-library-transact-sql.md)
[删除外部库 (Transact SQL)](drop-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)  
