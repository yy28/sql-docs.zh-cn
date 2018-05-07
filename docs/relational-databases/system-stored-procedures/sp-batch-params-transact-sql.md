---
title: sp_batch_params (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_batch_params
- sp_batch_params_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_batch_params
ms.assetid: 7b92fe9e-e755-4b7a-8a15-822c58a813d3
caps.latest.revision: 20
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: cf23ef8e7c0cb08f2cc87d8d76b5dc7145d244e0
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="spbatchparams-transact-sql"></a>sp_batch_params (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回包含有关中包含的参数的信息的行集[!INCLUDE[tsql](../../includes/tsql-md.md)]批处理。 **sp_batch_params**仅分析指定的批处理，并返回有关嵌入的参数值的信息。 此命令不会执行批处理，也不会修改执行环境。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_batch_params [ [ @tsqlbatch = ] 'tsqlbatch' ]   
```  
  
## <a name="arguments"></a>参数  
 [  **@tsqlbatch =**] *****tsqlbatch*****  
 是一个 Unicode 字符串，包含[!INCLUDE[tsql](../../includes/tsql-md.md)]语句或批处理哪些参数，将为所需信息。 *tsqlbatch*是**nvarchar (max)** 或隐式转换为**nvarchar (max)**。  
  
## <a name="return-code-values"></a>返回代码值  
 InclusionThresholdSetting  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**PARAMETER_NAME**|**sysname**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在批处理中找到的参数的名称。|  
|**COLUMN_TYPE**|**int**|此字段返回下列值之一：<br /><br /> 0 = SQL_PARAM_TYPE_UNKNOWN<br /><br /> 1 = SQL_PARAM_TYPE_INPUT<br /><br /> 2 = SQL_PARAM_TYPE_OUTPUT<br /><br /> 3 = SQL_RESULT_COL<br /><br /> 4 = SQL_PARAM_OUTPUT<br /><br /> 5 = SQL_RETURN_VALUE<br /><br /> 此列始终为 0。|  
|**DATA_TYPE**|**int**|参数的数据类型（ODBC 数据类型的整数代码）。 如果此数据类型无法映射到 ISO 类型，则值为 NULL。 在中返回的本机数据类型名称**TYPE_NAME**列。 此值始终为 NULL。|  
|**TYPE_NAME**|**sysname**|数据类型的字符串表示形式，通过基础 DBMS 提供。 此值为 NULL。|  
|**PRECISION**|**int**|有效数字位数。 返回值**精度**列是以 10 为基数。|  
|**LENGTH**|**int**|数据的传输大小。 此值为 NULL。|  
|**SCALE**|**int**|小数点右边的数字位数。 此值为 NULL。|  
|**RADIX**|**int**|数值类型的基数。 此值为 NULL。|  
|**可以为 NULL**|**int**|指定为空性：<br /><br /> 1 = 可以将参数数据类型创建为允许空值。<br /><br /> 0 = 不允许空值。<br /><br /> 此值为 NULL。|  
|**SQL_DATA_TYPE**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统数据类型的值，在说明符的 TYPE 字段中显示。 此列等同于**DATA_TYPE**列中，除**datetime**和 ISO**间隔**数据类型。 该列始终返回值。 此值为 NULL。|  
|**SQL_DATETIME_SUB**|**int**|**Datetime**或 ISO**间隔**如果子代码的值**SQL_DATA_TYPE** SQL_DATETIME 或 SQL_INTERVAL。 数据类型以外**datetime**和 ISO**间隔**，此列为 NULL。 此值为 NULL。|  
|**CHAR_OCTET_LENGTH**|**int**|以字节为单位的最大长度**字符**或**二进制**数据类型参数。 对于所有其他数据类型，此列返回 NULL。 此值始终为 NULL。|  
|**ORDINAL_POSITION**|**int**|参数在批处理中的顺序位置。 如果参数名称重复多次，则此列使用第一次出现的序号。 第一个参数的序号为 1。 该列始终返回值。|  
  
## <a name="permissions"></a>权限  
 执行的权限**sp_batch_params**权限已授予**公共**。  
  
## <a name="examples"></a>示例  
 以下示例显示了传递给 `sp_batch_params` 的一个查询。 结果集枚举了一组嵌入参数值。  
  
```  
DECLARE @SQLString nvarchar(500);  
/* Build the SQL string */  
SET @SQLString =  
     N'SELECT * FROM AdventureWorks2012.HumanResources.Employee   
     WHERE BusinessEntityID = @BusinessEntityID';  
EXECUTE sp_batch_params @SQLString;  
```  
  
## <a name="see-also"></a>另请参阅  
 [运行存储的过程](../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)   
 [运行存储的过程操作指南主题&#40;ODBC&#41;](http://msdn.microsoft.com/library/c2220182-a23d-4475-b353-77a77ab613d6)   
 [运行存储过程 & #40; OLE DB & #41;](../../relational-databases/native-client/ole-db/stored-procedures-running.md)  
  
  
