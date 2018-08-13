---
title: sys.external_file_formats (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a89efb2c-0a3a-4b64-9284-6e93263e29ac
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: dea0275fbdeea5dc413d4fc69a1da224cd2a6a04
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2018
ms.locfileid: "39560517"
---
# <a name="sysexternalfileformats-transact-sql"></a>sys.external_file_formats (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  在当前数据库中为每个外部文件格式存在对应的一行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]， [!INCLUDE[ssSDS](../../includes/sssds-md.md)]，和[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。  
  
 在服务器上针对每个外部文件格式存在对应的一行[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|file_format_id|**int**|外部文件格式的对象 ID。||  
|NAME|**sysname**|文件格式的名称。 在中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]，这是唯一的数据库。 在[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，这是唯一的服务器。||  
|format_type|**tinyint**|文件格式类型。|DELIMITEDTEXT，RCFILE、 ORC 和 PARQUET|  
|field_terminator|**nvarchar(10)**|Format_type = DELIMITEDTEXT，这是字段终止符。||  
|string_delimiter|**nvarchar(10)**|Format_type = DELIMITEDTEXT，这是字符串分隔符。||  
|date_format|**nvarchar(50)**|Format_type = DELIMITEDTEXT，这是用户定义的日期和时间格式。||  
|use_type_default|**bit**|Format_type = 分隔的文本、 指定如何处理缺失值，PolyBase 从 HDFS 文本文件到导入数据时[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。|0 – 将缺失值存储为字符串 NULL。<br /><br /> 1 – 将缺失值存储为列默认值。|  
|serde_method|**nvarchar(255)**|Format_type = RCFILE，这是序列化/反序列化方法。||  
|row_terminator|**nvarchar(10)**|Format_type = DELIMITEDTEXT，这是终止外部 Hadoop 文件中的每一行的字符字符串。|始终 ' \n'。|  
|编码|**nvarchar(10)**|Format_type = DELIMITEDTEXT，这是外部 Hadoop 文件的编码方法。|始终 UTF8。|  
|data_compression|**nvarchar(255)**|数据压缩方法为外部数据的。|Format_type = DELIMITEDTEXT:<br /><br /> -   'org.apache.hadoop.io.compress.DefaultCodec'<br />-   'org.apache.hadoop.io.compress.GzipCodec'<br /><br /> Format_type = RCFILE:<br /><br /> -   'org.apache.hadoop.io.compress.DefaultCodec'<br /><br /> Format_type = ORC:<br /><br /> -   'org.apache.hadoop.io.compress.DefaultCodec'<br />-   'org.apache.hadoop.io.compress.SnappyCodec'<br /><br /> Format_type = PARQUET:<br /><br /> -   'org.apache.hadoop.io.compress.GzipCodec'<br />-   'org.apache.hadoop.io.compress.SnappyCodec'|  
  
## <a name="permissions"></a>Permissions  
 目录视图中仅显示用户拥有的安全对象的元数据，或用户对其拥有某些权限的安全对象的元数据。 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>请参阅  
 [sys.external_data_sources &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md)   
 [sys.external_tables &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-tables-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](../../t-sql/statements/create-external-file-format-transact-sql.md)  
  
  
