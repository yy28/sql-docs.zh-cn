---
title: DECLARE CURSOR (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|language-elements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DECLARE_CURSOR_TSQL
- CURSOR_TSQL
- DECLARE CURSOR
- CURSOR
dev_langs:
- TSQL
helpviewer_keywords:
- DECLARE CURSOR statement
- cursors [SQL Server], attributes
- local cursors [SQL Server]
- nesting cursors
- Transact-SQL cursors, attributes
- global cursors [SQL Server]
ms.assetid: 5a3a27aa-03e8-4c98-a27e-809282379b21
caps.latest.revision: 51
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 42e3ae8b426b7230cf8cfee4be68838792d30318
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33064494"
---
# <a name="declare-cursor-transact-sql"></a>DECLARE CURSOR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  定义 [!INCLUDE[tsql](../../includes/tsql-md.md)] 服务器游标的属性，例如游标的滚动行为和用于生成游标所操作的结果集的查询。 DECLARE CURSOR 既接受基于 ISO 标准的语法，也接受使用一组 [!INCLUDE[tsql](../../includes/tsql-md.md)] 扩展的语法。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
ISO Syntax  
DECLARE cursor_name [ INSENSITIVE ] [ SCROLL ] CURSOR   
     FOR select_statement   
     [ FOR { READ ONLY | UPDATE [ OF column_name [ ,...n ] ] } ]  
[;]  
Transact-SQL Extended Syntax  
DECLARE cursor_name CURSOR [ LOCAL | GLOBAL ]   
     [ FORWARD_ONLY | SCROLL ]   
     [ STATIC | KEYSET | DYNAMIC | FAST_FORWARD ]   
     [ READ_ONLY | SCROLL_LOCKS | OPTIMISTIC ]   
     [ TYPE_WARNING ]   
     FOR select_statement   
     [ FOR UPDATE [ OF column_name [ ,...n ] ] ]  
[;]  
```  
  
## <a name="arguments"></a>参数  
 cursor_name  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 服务器游标定义的名称。 cursor_name 必须符合有关标识符的规则。  
  
 INSENSITIVE  
 定义一个游标，以创建将由该游标使用的数据的临时副本。 对游标的所有请求都从 tempdb 中的这一临时表中得到应答；因此，在对该游标进行提取操作时返回的数据中不反映对基表所做的修改，并且该游标不允许修改。 使用 ISO 语法时，如果省略 INSENSITIVE，则已提交的（任何用户）对基础表的删除和更新则会反映在后面的提取操作中。  
  
 SCROLL  
 指定所有的提取选项（FIRST、LAST、PRIOR、NEXT、RELATIVE、ABSOLUTE）均可用。 如果未在 ISO DECLARE CURSOR 中指定 SCROLL，则 NEXT 是唯一支持的提取选项。 如果也指定了 FAST_FORWARD，则不能指定 SCROLL。  
  
 select_statement  
 定义游标结果集的标准 SELECT 语句。 在游标声明的 select_statement 中不允许使用关键字 FOR BROWSE 和 INTO。  
  
 如果 select_statement 中的子句与所请求的游标类型的功能有冲突，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会将游标隐式转换为其他类型。  
  
 READ ONLY  
 禁止通过该游标进行更新。 在 UPDATE 或 DELETE 语句的 WHERE CURRENT OF 子句中不能引用游标。 该选项优先于要更新的游标的默认功能。  
  
 UPDATE [OF column_name [,...n]]  
 定义游标中可更新的列。 如果指定了 OF column_name [,...n]，则只允许修改所列出的列。 如果指定了 UPDATE，但未指定列的列表，则可以更新所有列。  
  
 cursor_name  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 服务器游标定义的名称。 cursor_name 必须符合有关标识符的规则。  
  
 LOCAL  
 指定该游标的范围对在其中创建它的批处理、存储过程或触发器是局部的。 该游标名称仅在这个作用域内有效。 在批处理、存储过程、触发器或存储过程 OUTPUT 参数中，该游标可由局部游标变量引用。 OUTPUT 参数用于将局部游标传递回调用批处理、存储过程或触发器，它们可在存储过程终止后给游标变量分配参数使其引用游标。 除非 OUTPUT 参数将游标传递回来，否则游标将在批处理、存储过程或触发器终止时隐式释放。 如果 OUTPUT 参数将游标传递回来，则游标在最后引用它的变量释放或离开作用域时释放。  
  
 GLOBAL  
 指定该游标范围对连接是全局的。 在由此连接执行的任何存储过程或批处理中，都可以引用该游标名称。 该游标仅在断开连接时隐式释放。  
  
> [!NOTE]  
>  如果 GLOBAL 和 LOCAL 参数都未指定，则默认值由 default to local cursor 数据库选项的设置控制。  
  
 FORWARD_ONLY  
 指定游标只能从第一行滚动到最后一行。 FETCH NEXT 是唯一支持的提取选项。 如果在指定 FORWARD_ONLY 时不指定 STATIC、KEYSET 和 DYNAMIC 关键字，则游标作为 DYNAMIC 游标进行操作。 如果 FORWARD_ONLY 和 SCROLL 均未指定，那么除非指定了 STATIC、KEYSET 或 DYNAMIC 关键字，否则默认值为 FORWARD_ONLY。 STATIC、KEYSET 和 DYNAMIC 游标默认为 SCROLL。 与 ODBC 和 ADO 这类数据库 API 不同，STATIC、KEYSET 和 DYNAMIC [!INCLUDE[tsql](../../includes/tsql-md.md)] 游标支持 FORWARD_ONLY。  
  
 STATIC  
 定义一个游标，以创建将由该游标使用的数据的临时副本。 对游标的所有请求都从 tempdb 中的这一临时表中得到应答；因此，在对该游标进行提取操作时返回的数据中不反映对基表所做的修改，并且该游标不允许修改。  
  
 KEYSET  
 指定当游标打开时，游标中行的成员身份和顺序已经固定。 对行进行唯一标识的键集内置在 tempdb 内一个称为 keyset 的表中。  
  
> [!NOTE]  
>  如果查询引用了至少一个无唯一索引的表，则键集游标将转换为静态游标。  
  
 对基表中的非键值所做的更改（由游标所有者更改或由其他用户提交）可以在用户滚动游标时看到。 其他用户执行的插入是不可见的（不能通过 [!INCLUDE[tsql](../../includes/tsql-md.md)] 服务器游标执行插入）。 如果删除某一行，则在尝试提取该行时返回的 @@FETCH_STATUS 为 -2。 从游标外部更新键值类似于删除旧行后再插入新行。 具有新值的行不可见，且尝试提取具有旧值的行时返回的 @@FETCH_STATUS 为 -2。 如果通过指定 WHERE CURRENT OF 子句来通过游标执行更新，则新值可见。  
  
 DYNAMIC  
 定义一个游标，以反映在滚动游标时对结果集内的各行所做的所有数据更改。 行的数据值、顺序和成员身份在每次提取时都会更改。 动态游标不支持 ABSOLUTE 提取选项。  
  
 FAST_FORWARD  
 指定启用了性能优化的 FORWARD_ONLY、READ_ONLY 游标。 如果指定了 SCROLL 或 FOR_UPDATE，则不能也指定 FAST_FORWARD。  
  
> [!NOTE]  
>  FAST_FORWARD 和 FORWARD_ONLY 可以同时用在同一个 DECLARE CURSOR 语句中。  
  
 READ_ONLY  
 禁止通过该游标进行更新。 在 UPDATE 或 DELETE 语句的 WHERE CURRENT OF 子句中不能引用游标。 该选项优先于要更新的游标的默认功能。  
  
 SCROLL_LOCKS  
 指定通过游标进行的定位更新或删除一定会成功。 将行读入游标时 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将锁定这些行，以确保随后可对它们进行修改。 如果还指定了 FAST_FORWARD 或 STATIC，则不能指定 SCROLL_LOCKS。  
  
 OPTIMISTIC  
 指定如果行自读入游标以来已得到更新，则通过游标进行的定位更新或定位删除不成功。 当将行读入游标时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不锁定行。 相反，它使用 timestamp 列值的比较，或者如果表没有 timestamp 列则使用校验和值，以确定将行读入游标后是否已修改该行。 如果已修改该行，尝试进行的定位更新或定位删除将失败。 如果还指定了 FAST_FORWARD，则不能指定 OPTIMISTIC。  
  
 TYPE_WARNING  
 指定如果游标从所请求的类型隐式转换为另一种类型，则向客户端发送警告消息。  
  
 select_statement  
 定义游标结果集的标准 SELECT 语句。 在游标声明的 select_statement 中不允许使用关键字 COMPUTE、COMPUTE BY、FOR BROWSE 和 INTO。  
  
> [!NOTE]  
>  可以在游标声明中使用查询提示；但如果还使用了 FOR UPDATE OF 子句，则请在 FOR UPDATE OF 之后指定 OPTION (query_hint)。  
  
 如果 select_statement 中的子句与所请求的游标类型的功能有冲突，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 会将游标隐式转换为其他类型。 有关详细信息，请参阅“隐式游标转换”。  
  
 FOR UPDATE [OF column_name [,...n]]  
 定义游标中可更新的列。 如果提供了 OF column_name [,...n]，则只允许修改列出的列。 如果指定了 UPDATE，但未指定列的列表，则除非指定了 READ_ONLY 并发选项，否则可以更新所有的列。  
  
## <a name="remarks"></a>Remarks  
 DECLARE CURSOR 定义 [!INCLUDE[tsql](../../includes/tsql-md.md)] 服务器游标的属性，例如游标的滚动行为和用于生成游标所操作的结果集的查询。 OPEN 语句填充结果集，FETCH 从结果集返回行。 CLOSE 语句释放与游标关联的当前结果集。 DEALLOCATE 语句释放游标所使用的资源。  
  
 DECLARE CURSOR 语句的第一种格式采用 ISO 语法来声明游标行为。 DECLARE CURSOR 的第二种格式使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 扩展插件，这些扩展插件允许您使用在 ODBC 或 ADO 的数据库 API 游标函数中所使用的相同游标类型来定义游标。  
  
 不能混淆这两种格式。 如果在 CURSOR 关键字前指定 SCROLL 或 INSENSITIVE 关键字，则不能在 CURSOR 和 FOR select_statement 关键字之间使用任何关键字。 如果在 CURSOR 和 FOR select_statement 关键字之间指定任何关键字，则不能在 CURSOR 关键字前指定 SCROLL 或 INSENSITIVE。  
  
 如果使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语法的 DECLARE CURSOR 不指定 READ_ONLY、OPTIMISTIC 或 SCROLL_LOCKS，则默认值如下：  
  
-   如果 SELECT 语句不支持更新（由于权限不够、访问的远程表不支持更新等等），则游标为 READ_ONLY。  
  
-   STATIC 和 FAST_FORWARD 游标默认为 READ_ONLY。  
  
-   DYNAMIC 和 KEYSET 游标默认为 OPTIMISTIC。  
  
 游标名称只能被其他 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句引用。 它们不能被数据库 API 函数引用。 例如，声明游标之后，不能通过 OLE DB、ODBC 或 ADO 函数或方法引用游标名称。 不能使用 API 的提取函数或方法来提取游标行；只能通过 [!INCLUDE[tsql](../../includes/tsql-md.md)] FETCH 语句提取这些行。  
  
 在声明游标后，可使用下列系统存储过程确定游标的特性。  
  
|系统存储过程|Description|  
|------------------------------|-----------------|  
|**sp_cursor_list**|返回当前在连接上可视的游标列表及其特性。|  
|**sp_describe_cursor**|说明游标属性，例如是只前推的游标还是滚动游标。|  
|**sp_describe_cursor_columns**|说明游标结果集中的列的属性。|  
|**sp_describe_cursor_tables**|说明游标所访问的基表。|  
  
 在声明游标的 select_statement 中可以使用变量。 游标变量值在声明游标后不发生更改。  
  
## <a name="permissions"></a>权限  
 默认情况下，将 DECLARE CURSOR 权限授予对游标中所使用的视图、表和列具有 SELECT 权限的任何用户。
 
## <a name="limitations-and-restrictions"></a>限制和局限

不能在具有聚集列存储索引的表中使用游标或触发器。 此限制不适用于非聚集列存储索引；可以在具有非聚集列存储索引的表中使用游标和触发器。 
  
## <a name="examples"></a>示例  
  
### <a name="a-using-simple-cursor-and-syntax"></a>A. 使用简单的游标和语法  

在打开该游标时所生成的结果集包括表中的所有行和所有列。 可以更新该游标，并且所有的更新和删除都会在对该游标所做的提取操作中表现出来。 `FETCH NEXT` 是唯一可用的提取选项，因为未指定 `SCROLL` 选项。  

  
```  
DECLARE vend_cursor CURSOR  
    FOR SELECT * FROM Purchasing.Vendor  
OPEN vend_cursor  
FETCH NEXT FROM vend_cursor;  
```  
  
### <a name="b-using-nested-cursors-to-produce-report-output"></a>B. 使用嵌套游标生成报表输出  
 下例说明如何通过嵌套游标生成复杂的报表。 为每个供应商声明内部游标。  
  
```  
SET NOCOUNT ON;  
  
DECLARE @vendor_id int, @vendor_name nvarchar(50),  
    @message varchar(80), @product nvarchar(50);  
  
PRINT '-------- Vendor Products Report --------';  
  
DECLARE vendor_cursor CURSOR FOR   
SELECT VendorID, Name  
FROM Purchasing.Vendor  
WHERE PreferredVendorStatus = 1  
ORDER BY VendorID;  
  
OPEN vendor_cursor  
  
FETCH NEXT FROM vendor_cursor   
INTO @vendor_id, @vendor_name  
  
WHILE @@FETCH_STATUS = 0  
BEGIN  
    PRINT ' '  
    SELECT @message = '----- Products From Vendor: ' +   
        @vendor_name  
  
    PRINT @message  
  
    -- Declare an inner cursor based     
    -- on vendor_id from the outer cursor.  
  
    DECLARE product_cursor CURSOR FOR   
    SELECT v.Name  
    FROM Purchasing.ProductVendor pv, Production.Product v  
    WHERE pv.ProductID = v.ProductID AND  
    pv.VendorID = @vendor_id  -- Variable value from the outer cursor  
  
    OPEN product_cursor  
    FETCH NEXT FROM product_cursor INTO @product  
  
    IF @@FETCH_STATUS <> 0   
        PRINT '         <<None>>'       
  
    WHILE @@FETCH_STATUS = 0  
    BEGIN  
  
        SELECT @message = '         ' + @product  
        PRINT @message  
        FETCH NEXT FROM product_cursor INTO @product  
        END  
  
    CLOSE product_cursor  
    DEALLOCATE product_cursor  
        -- Get the next vendor.  
    FETCH NEXT FROM vendor_cursor   
    INTO @vendor_id, @vendor_name  
END   
CLOSE vendor_cursor;  
DEALLOCATE vendor_cursor;  
```  
  
## <a name="see-also"></a>另请参阅  
 [@@FETCH_STATUS (Transact-SQL)](../../t-sql/functions/fetch-status-transact-sql.md)   
 [CLOSE (Transact-SQL)](../../t-sql/language-elements/close-transact-sql.md)   
 [游标 (Transact-SQL)](../../t-sql/language-elements/cursors-transact-sql.md)   
 [DEALLOCATE (Transact-SQL)](../../t-sql/language-elements/deallocate-transact-sql.md)   
 [FETCH (Transact-SQL)](../../t-sql/language-elements/fetch-transact-sql.md)   
 [SELECT (Transact-SQL)](../../t-sql/queries/select-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
