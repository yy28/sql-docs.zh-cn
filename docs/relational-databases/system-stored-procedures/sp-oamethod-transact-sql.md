---
title: "sp_OAMethod (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_OAMethod
- sp_OAMethod_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_OAMethod
ms.assetid: 1dfaebe2-c7cf-4041-a586-5d04faf2e25e
caps.latest.revision: "25"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0dcf9235953ca1e907c4bae97562d5ea0a00049b
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2017
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
 通过使用先前创建的 OLE 对象的对象标记**sp_OACreate**。  
  
 *方法名称*  
 要调用的 OLE 对象的方法名。  
  
 *returnvalue***输出**   
 OLE 对象的方法的返回值。 如果指定此参数，则必须是相应数据类型的局部变量。  
  
 如果该方法返回单个值，请指定的本地变量*returnvalue*，这将返回该方法在本地的变量中，返回值或不指定*returnvalue*，它将返回方法就是单列、 单行结果集值返回到客户端。  
  
 如果此方法返回值是一个 OLE 对象， *returnvalue*必须是数据类型的本地变量**int**。对象令牌保存在该局部变量中，并且此对象令牌可用于其他 OLE 自动化存储过程。  
  
 当该方法返回值是一个数组，如果*returnvalue*指定，则设置为 NULL。  
  
 如果出现下列任意一种情况，则产生错误：  
  
-   *returnvalue*指定，但该方法不返回值。  
  
-   方法返回二维以上的数组。  
  
-   方法返回一个数组作为输出参数。  
  
 [  *@parametername*   **=**  ]*参数*[**输出**]  
 一个方法参数。 如果指定，*参数*必须是适当的数据类型的值。  
  
 若要获取输出参数，返回值*参数*必须适当的数据类型，是本地变量和**输出**必须指定。 如果指定常量参数，或如果**输出**未指定，则任何返回值从一个输出参数将被忽略。  
  
 如果指定， *parametername*必须是的名称[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]命名参数。 请注意，  **@**  *parametername*不[!INCLUDE[tsql](../../includes/tsql-md.md)]本地变量。 At 符号 (**@**) 被删除，和*parametername*传递给 OLE 对象作为参数名称。 指定了所有位置参数后，才能指定命名参数。  
  
 *n*  
 指示可以指定多个参数的占位符。  
  
> [!NOTE]  
>  *@parametername*可以是方法的一个命名的参数，因为它是方法的指定的一部分，并通过传递给对象。 此存储过程的其他参数是按位置（而不是名称）指定的。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或非零数字（失败），是由 OLE 自动化对象返回的 HRESULT 整数值。  
  
 HRESULT 返回代码，有关详细信息[OLE 自动化返回代码和错误信息](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md)。  
  
## <a name="result-sets"></a>结果集  
 如果方法返回值是一维或二维数组，那么该数组将作为结果集返回给客户端：  
  
-   一维数组作为单行结果集返回给客户端，其中的列数与数组中的元素数相等。 换言之，该数组以（列）的形式返回。  
  
-   二维数组作为结果集返回给客户端，其中的列数与数组第一维中的元素数相同，行数与数组第二维中的元素数相同。 换言之，该数组以（列、行）的形式返回。  
  
 当属性返回值或方法返回值是一个数组， **sp_OAGetProperty**或**sp_OAMethod**返回的结果集向客户端。 （方法输出参数不能是数组。这些过程可扫描数组中的所有数据值，以确定用于结果集中各列的相应 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据类型和数据长度。 对于某个特定的列，这些过程将使用显示该列中的所有数据值所需要的数据类型和长度。  
  
 如果一列中的所有数据值具有相同的数据类型，此数据类型将用于整个列。 当列中的数据值为其他数据类型时，将基于下表选择整个列的数据类型。  
  
||int|float|money|datetime|varchar|nvarchar|  
|------|---------|-----------|-----------|--------------|-------------|--------------|  
|**int**|**int**|**float**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**float**|**float**|**float**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**money**|**money**|**money**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**datetime**|**varchar**|**varchar**|**varchar**|**datetime**|**varchar**|**nvarchar**|  
|**varchar**|**varchar**|**varchar**|**varchar**|**varchar**|**varchar**|**nvarchar**|  
|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|  
  
## <a name="remarks"></a>注释  
 你还可以使用**sp_OAMethod**来获取属性值。  
  
## <a name="permissions"></a>Permissions  
 要求具有 **sysadmin** 固定服务器角色的成员身份。  
  
## <a name="examples"></a>示例  
  
### <a name="a-calling-a-method"></a>A. 调用一个方法  
 下面的示例调用`Connect`以前创建的方法**SQLServer**对象。  
  
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
 下面的示例获取`HostName`属性 (以前创建的**SQLServer**对象) 并将其存储在本地变量。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [OLE 自动化存储过程 &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [OLE 自动化脚本示例](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
