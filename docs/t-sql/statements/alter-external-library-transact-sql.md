---
title: "ALTER 外部库 (Transact SQL) |Microsoft 文档"
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
- ALTER EXTERNAL LIBRARY
- ALTER_EXTERNAL_LIBRARY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER EXTERNAL LIBRARY
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 541419770828e01cca82fb33ead1b22170f8e4f3
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="alter-external-library-transact-sql"></a>ALTER 外部库 (Transact SQL)  
[!INCLUDE[tsql-appliesto-ssvnxt-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]  

修改现有库内容。  

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

**平台 = WINDOWS**

指定内容库的平台。 修改现有的库来添加不同的平台时，此值是必需的。 Windows 是唯一受支持的平台。

## <a name="remarks"></a>注释

对于 R 语言中，包必须准备与压缩的存档文件的形式。适用于 Windows 的 ZIP 扩展。 目前，支持仅 Windows 平台。  
`ALTER EXTERNAL LIBRARY`语句仅将库 bits 上载到数据库。 已修改的库用户运行的外部脚本之后，通过执行之前未实际安装[sp_execute_external_script (TRANSACT-SQL)](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。

## <a name="permissions"></a>Permissions
需要`ALTER ANY EXTERNAL LIBRARY`权限。 创建外部库，用户可以更改该外部的库。

## <a name="examples"></a>示例

下面的示例修改了名为 customPackage 外部库。

```sql  
ALTER EXTERNAL LIBRARY customPackage 
SET 
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


## <a name="see-also"></a>另请参阅  
[创建外部库 (Transact SQL)](create-external-library-transact-sql.md)
[删除外部库 (Transact SQL)](drop-external-library-transact-sql.md)  
[sys.external_library_files](../../relational-databases/system-catalog-views/sys-external-library-files-transact-sql.md)  
[sys.external_libraries](../../relational-databases/system-catalog-views/sys-external-libraries-transact-sql.md)  

