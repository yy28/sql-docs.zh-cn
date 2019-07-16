---
title: sp_OAMethod (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_OAMethod
- sp_OAMethod_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_OAMethod
ms.assetid: 1dfaebe2-c7cf-4041-a586-5d04faf2e25e
author: stevestein
ms.author: sstein
ms.openlocfilehash: c7dbc0d6ccf753f8f11baee2f5c1c479895d0687
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107918"
---
# <a name="spoamethod-transact-sql"></a>sp_OAMethod (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  调用一个 OLE 对象的方法。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_OAMethod objecttoken , methodname  
    [ , returnvalue OUTPUT ]   
    [ , [ @parametername = ] parameter [ OUTPUT ] [ ...n ] ]   
```  
  
## <a name="arguments"></a>参数  
 *objecttoken*  
 通过使用先前创建的 OLE 对象的对象令牌**sp_OACreate**。  
  
 *methodname*  
 要调用的 OLE 对象的方法名。  
  
 _returnvalue_ **输出**  
 OLE 对象的方法的返回值。 如果指定此参数，则必须是相应数据类型的局部变量。  
  
 如果该方法返回单个值，指定的局部变量*returnvalue*，这会返回该方法在本地变量中，返回值或不指定*returnvalue*，它将返回方法作为单列、 单行结果集返回到客户端的值。  
  
 如果该方法的返回值是 OLE 对象， *returnvalue*必须是数据类型的本地变量**int**。一个对象标记标记存储在本地变量，此对象令牌可用于其他 OLE 自动化存储过程。  
  
 如果方法返回值是一个数组，如果*returnvalue*指定，则设置为 NULL。  
  
 如果出现下列任意一种情况，则产生错误：  
  
-   *returnvalue*指定，但该方法不返回值。  
  
-   方法返回二维以上的数组。  
  
-   方法返回一个数组作为输出参数。  
  
`[ _@parametername = ] parameter[ OUTPUT ]` 为方法参数。 如果指定，*参数*必须是相应的数据类型的值。  
  
 若要获取输出参数，返回值*参数*必须是相应的数据类型的本地变量和**输出**必须指定。 如果指定常数参数，或如果**输出**未指定，则任何返回输出参数的值将被忽略。  
  
 如果指定， *parametername*必须是名称[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]命名参数。 请注意， **@** _parametername_is 不[!INCLUDE[tsql](../../includes/tsql-md.md)]本地变量。 At 符号 ( **@** ) 中删除，并且*parametername*传递给 OLE 对象作为参数名称。 指定了所有位置参数后，才能指定命名参数。  
  
 *n*  
 指示可以指定多个参数的占位符。  
  
> [!NOTE]
>  *@parametername* 可以是一个命名的参数，因为它是指定方法的一部分，并且将传递给该对象。 此存储过程的其他参数是按位置（而不是名称）指定的。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或非零数字（失败），是由 OLE 自动化对象返回的 HRESULT 整数值。  
  
 HRESULT 返回代码，有关详细信息[OLE 自动化返回代码和错误信息](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md)。  
  
## <a name="result-sets"></a>结果集  
 如果方法返回值是一维或二维数组，那么该数组将作为结果集返回给客户端：  
  
-   一维数组作为单行结果集返回给客户端，其中的列数与数组中的元素数相等。 换言之，该数组以（列）的形式返回。  
  
-   二维数组作为结果集返回给客户端，其中的列数与数组第一维中的元素数相同，行数与数组第二维中的元素数相同。 换言之，该数组以（列、行）的形式返回。  
  
 当属性返回值或方法返回值是一个数组， **sp_OAGetProperty**或**sp_OAMethod**结果集返回到客户端。 （方法输出参数不能是数组。这些过程可扫描数组中的所有数据值，以确定用于结果集中各列的相应 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型和数据长度。 对于某个特定的列，这些过程将使用显示该列中的所有数据值所需要的数据类型和长度。  
  
 如果一列中的所有数据值具有相同的数据类型，此数据类型将用于整个列。 当列中的数据值为其他数据类型时，将基于下表选择整个列的数据类型。  
  
||INT|FLOAT|money|DATETIME|varchar|NVARCHAR|  
|------|---------|-----------|-----------|--------------|-------------|--------------|  
|**int**|**int**|**float**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**float**|**float**|**float**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**money**|**money**|**money**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**datetime**|**varchar**|**varchar**|**varchar**|**datetime**|**varchar**|**nvarchar**|  
|**varchar**|**varchar**|**varchar**|**varchar**|**varchar**|**varchar**|**nvarchar**|  
|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|  
  
## <a name="remarks"></a>备注  
 此外可以使用**sp_OAMethod**获取属性值。  
  
## <a name="permissions"></a>权限  
 要求的成员身份**sysadmin**固定服务器角色或直接在此存储过程的执行权限。 `Ole Automation Procedures` 必须配置**启用**若要使用相关的 OLE 自动化到任何系统过程。  
  
## <a name="examples"></a>示例  
  
### <a name="a-calling-a-method"></a>A. 调用一个方法  
 下面的示例调用`Connect`先前创建的方法**SQLServer**对象。  
  
```  
EXEC @hr = sp_OAMethod @object, 'Connect', NULL, 'my_server',  
    'my_login', 'my_password';  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object  
    RETURN  
END;  
```  
  
### <a name="b-getting-a-property"></a>B. 获取一个属性  
 下面的示例获取`HostName`属性 (先前创建的**SQLServer**对象) 并将其存储在本地变量。  
  
```  
DECLARE @property varchar(255);  
EXEC @hr = sp_OAMethod @object, 'HostName', @property OUT;  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object  
    RETURN  
END;  
PRINT @property;  
```  
  
## <a name="see-also"></a>请参阅  
 [OLE 自动化存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [OLE 自动化脚本示例](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
