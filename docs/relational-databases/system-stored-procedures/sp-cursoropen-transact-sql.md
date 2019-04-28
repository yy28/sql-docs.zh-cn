---
title: sp_cursoropen (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursoropen
- sp_cursoropen_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursoropen
ms.assetid: 16462ede-4393-4293-a598-ca88c48ca70b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7410371f7d96f9770536a129de3a916b5f297a74
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62724021"
---
# <a name="spcursoropen-transact-sql"></a>sp_cursoropen (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  将打开一个游标。 sp_cursoropen 定义与游标和游标选项相关联的 SQL 语句，然后填充游标。 sp_cursoropen 相当于的组合[!INCLUDE[tsql](../../includes/tsql-md.md)]语句 DECLARE_CURSOR 和 OPEN。 此过程通过在表格格式数据流 (TDS) 数据包中指定 ID = 2 来调用。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_cursoropen cursor OUTPUT, stmt  
    [, scrollopt[ OUTPUT ] [ , ccopt[ OUTPUT ]  
    [ ,rowcount OUTPUT [ ,boundparam][,...n]]] ]]  
```  
  
## <a name="arguments"></a>参数  
 *cursor*  
 SQL Server 生成的游标标识符。 *游标*是*处理*必须对涉及游标，如 sp_cursorfetch 的所有后续过程中提供的值。 *游标*为必需的参数且具有**int**返回值。  
  
 *游标*允许多个游标在单个数据库连接上处于活动状态。  
  
 *stmt*  
 定义游标结果集的必需参数。 任何字符串类型 （无论 Unicode、 大小等) 的任何有效的查询字符串 （语法和绑定） 可以作为有效*stmt*值类型。  
  
 *scrollopt*  
 滚动选项。 *scrollopt*是一个可选参数，需要以下项之一**int**输入值。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|0x0001|KEYSET|  
|0x0002|DYNAMIC|  
|0x0004|FORWARD_ONLY|  
|0x0008|STATIC|  
|0x10|FAST_FORWARD|  
|0x1000|PARAMETERIZED_STMT|  
|0x2000|AUTO_FETCH|  
|0x4000|AUTO_CLOSE|  
|0x8000|CHECK_ACCEPTED_TYPES|  
|0x10000|KEYSET_ACCEPTABLE|  
|0x20000|DYNAMIC_ACCEPTABLE|  
|0x40000|FORWARD_ONLY_ACCEPTABLE|  
|0x80000|STATIC_ACCEPTABLE|  
|0x100000|FAST_FORWARD_ACCEPTABLE|  
  
 由于可能存在的请求的值不适合于通过定义的游标*stmt*，此参数可同时用作输入和输出。 在此类情况下，SQL Server 分配一个适当的值。  
  
 *ccopt*  
 并发控制选项。 *ccopt*是一个可选参数，需要以下项之一**int**输入值。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|0x0001|READ_ONLY|  
|0x0002|SCROLL_LOCKS（以前称为 LOCKCC）|  
|0x0004|**乐观**（以前称为 OPTCC）|  
|0x0008|OPTIMISTIC（以前称为 OPTCCVAL）|  
|0x2000|ALLOW_DIRECT|  
|0x4000|UPDT_IN_PLACE|  
|0x8000|CHECK_ACCEPTED_OPTS|  
|0x10000|READ_ONLY_ACCEPTABLE|  
|0x20000|SCROLL_LOCKS_ACCEPTABLE|  
|0x40000|OPTIMISTIC_ACCEPTABLE|  
|0x80000|OPTIMISITC_ACCEPTABLE|  
  
 如同*scrollopt*，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可以重写请求*ccopt*值。  
  
 *rowcount*  
 要用于 AUTO_FETCH 的提取缓冲区行数。 默认值为 20 行。 *行计数*以不同的方式指定为输入值与返回值时的行为。  
  
|作为输入值|作为返回值|  
|--------------------|---------------------|  
|当 AUTO_FETCH *scrollopt*指定值*rowcount*表示要放入提取缓冲区的行数。<br /><br /> 注意： > AUTO_FETCH 指定了，但将忽略此设置，0 是有效的值。|表示结果的行数设置，除非*scrollopt*指定 AUTO_FETCH 值。|  
  
-  
  
 *boundparam*  
 指示使用其他参数。 *boundparam*是一个可选参数，如果应指定*scrollopt* PARAMETERIZED_STMT 值设置为 ON。  
  
## <a name="return-code-values"></a>返回代码值  
 如果未引发错误，则 sp_cursoropen 返回以下值之一。  
  
 0  
 已成功执行该过程。  
  
 0x0001  
 在执行过程中发生了错误（次要错误，严重程度不足以在操作中引发错误）。  
  
 0x0002  
 正在执行异步操作。  
  
 0x0002  
 正在执行 FETCH 操作。  
  
 A  
 此游标已由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 取消分配而不可用。  
  
 当引发错误时，返回值可能不一致，无法确保准确性。  
  
 当*rowcount*参数指定为返回值，则出现以下结果集。  
  
 -1  
 如果行数未知或不适用，则返回此值。  
  
 -n  
 当异步填充生效时，返回此值。 表示已放入提取的行数何时缓冲*scrollopt*指定 AUTO_FETCH 值。  
  
 如果使用 RPC，则返回值如下所示。  
  
 0  
 过程成功。  
  
 1  
 过程失败。  
  
 2  
 正在异步生成键集游标。  
  
 16  
 快进游标已自动关闭。  
  
> [!NOTE]  
>  如果成功执行了 sp_cursoropen 过程，RPC 返回参数和结果集具有 TDS 列格式信息 (0xa0 和 0xa1 消息) 发送。 如果不成功，则发送一条或多条 TDS 错误消息。 在任一情况下，将不返回任何行数据并*完成*消息计数将为零。 如果您使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本低于 7.0，将返回 0xa0、0xa1（SELECT 语句的标准）以及 0xa5 和 0xa4 标记流。 如果您使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0，将返回 0x81（SELECT 语句的标准）以及 0xa5 和 0xa4 标记流。  
  
## <a name="remarks"></a>备注  
  
## <a name="stmt-parameter"></a>stmt 参数  
 如果*stmt*指定执行存储过程的输入的参数可能要么定义为常量作为的一部分*stmt*字符串，或指定为*boundparam*自变量。 通过此方法，可以将声明的变量作为绑定参数传递。  
  
 允许的内容*stmt*参数取决于是否*ccopt* ALLOW_DIRECT 返回值具有已由 OR 链接到的其余部分*ccopt*值，即：  
  
-   如果 ALLOW_DIRECT 未指定，要么[!INCLUDE[tsql](../../includes/tsql-md.md)]SELECT 或 EXECUTE 语句调用必须使用包含单个 SELECT 语句的存储的过程。 此外，SELECT 语句必须限定为一个游标;也就是说，不能包含关键字 SELECT INTO 或 FOR BROWSE。  
  
-   如果指定了 ALLOW_DIRECT，则这可能导致一个或多个 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句，包括那些依次执行其他存储过程以及多个语句的语句。 将只执行非 SELECT 语句或包含关键字 SELECT INTO 或 FOR BROWSE 的任何 SELECT 语句，而不会导致创建游标。 这同样适用于在一批多个语句中包含的任何 SELECT 语句。 在 SELECT 语句包含只与游标相关的子句的情况下，将忽略这些子句。 例如，如果的值*ccopt*是 0x2002，这是用于请求：  
  
    -   具有滚动锁的游标（如果只有一个 SELECT 语句限定为游标），或者  
  
    -   一个直接的语句执行（如果有多个语句、一个非 SELECT 语句或不限定为游标的 SELECT 语句）。  
  
## <a name="scrollopt-parameter"></a>scrollopt 参数  
 前五个*scrollopt*值 （KEYSEY、 DYNAMIC、 FORWARD_ONLY、 静态的和 FAST_FORWARD） 是互斥。  
  
 PARAMETERIZED_STMT 和 CHECK_ACCEPTED_TYPES 可以由 OR 链接到前五个值中的任何一个。  
  
 AUTO_FETCH 和 AUTO_CLOSE 可以由 OR 链接到 FAST_FORWARD。  
  
 如果 CHECK_ACCEPTED_TYPES 为 ON，至少一个最后五*scrollopt*值 (KEYSET_ACCEPTABLE`,` DYNAMIC_ACCEPTABLE、 FORWARD_ONLY_ACCEPTABLE、 STATIC_ACCEPTABLE 或 FAST_FORWARD_ACCEPTABLE) 必须也为 ON。  
  
 STATIC 游标始终打开为 READ_ONLY。 这意味着无法通过此游标更新基础表。  
  
## <a name="ccopt-parameter"></a>ccopt 参数  
 前四个*ccopt*是互斥的值 （READ_ONLY、 SCROLL_LOCKS 和两个 OPTIMISTIC 值）。  
  
> [!NOTE]  
>  选择前四个之一*ccopt*值决定了游标是只读的或如果锁定或乐观方法可用来防止丢失的更新。 如果*ccopt*未指定值，默认值为 OPTIMISTIC。  
  
 ALLOW_DIRECT 和 CHECK_ACCEPTED_TYPES 可以由 OR 链接到前四个值中的任何一个。  
  
 UPDT_IN_PLACE 可以由 OR 链接到 READ_ONLY、SCROLL_LOCKS 或任一 OPTIMISTIC 值。  
  
 如果 CHECK_ACCEPTED_TYPES 为 ON，至少一个最后四个*ccopt*值 （READ_ONLY_ACCEPTABLE、 SCROLL_LOCKS_ACCEPTABLE 和任一 OPTIMISTIC_ACCEPTABLE 值） 必须也为 ON。  
  
 可能仅在提取缓冲区且仅当执行定位的 UPDATE 和 DELETE 函数*ccopt*值等于 SCROLL_LOCKS 或 OPTIMISTIC。 如果 SCROLL_LOCKS 是指定的值，则此操作可确保成功。 如果 OPTIMISTIC 是指定的值，则当自上次提取该行后行已发生变化时，操作将失败。  
  
 失败原因在于：当 OPTIMISTIC 为指定的值时，将通过比较时间戳或校验和值执行乐观并发控制函数（由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 确定）。 如果任何行不匹配，则操作失败。  
  
 将 UPDT_IN_PLACE 指定为返回值可控制以下结果：  
  
-   如果未设置，则当对某个表使用唯一索引执行定位更新时，游标将从其工作表中删除该行，并将其插入到游标使用的任何键列的末尾，从而更改这些列。  
  
-   如果设置为 ON，游标将只更新工作表的原始行中的键列。  
  
## <a name="boundparam-parameter"></a>bound_param 参数  
 参数名称应*paramdef*指定了 PARAMETERIZED_STMT 时，根据代码中的错误消息。 当未指定 PARAMETERIZED_STMT 时，在错误消息将不指定任何名称。  
  
## <a name="rpc-considerations"></a>RPC 注意事项  
 RPC RETURN_METADATA 输入标志可设置为 0x0001，以请求在 TDS 流中返回游标选择列表元数据。  
  
## <a name="examples"></a>示例  
  
### <a name="boundparam-parameter"></a>bound_param 参数  
 第五个参数之后的任何参数都将作为输入参数传递到语句计划。 第一个此类参数必须为以下格式的字符串：  
  
 *{ local variable name data type } [,...n]*  
  
 后续参数用于传递的值的替换*局部变量名*语句中。  
  
## <a name="see-also"></a>请参阅  
 [sp_cursorfetch &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursorfetch-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
