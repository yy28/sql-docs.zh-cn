---
title: "FORMATMESSAGE (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/12/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FORMATMESSAGE
- FORMATMESSAGE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmessages system table
- sys.messages catalog view
- FORMATMESSAGE function
- messages [SQL Server], formats
- errors [SQL Server], formats
ms.assetid: 83f18102-2035-4a87-acd0-8d96d03efad5
caps.latest.revision: 39
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 071f6def07baf0b74919fd5ce93e65494877dda0
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="formatmessage-transact-sql"></a>FORMATMESSAGE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  构造一条消息的 sys.messages 中现有消息或从提供的字符串。 FORMATMESSAGE 的功能与 RAISERROR 语句的功能类似。 但是，RAISERROR 会立即打印消息，而 FORMATMESSAGE 则返回供进一步处理的格式化消息。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
FORMATMESSAGE ( { msg_number  | ' msg_string ' } , [ param_value [ ,...n ] ] )  
```  
  
## <a name="arguments"></a>参数  
 *msg_number*  
 是存储在 sys.messages 的 ID。 如果*msg_number*是 < = 13000，或如果 sys.messages 中不存在消息，则返回 NULL。  
  
 *msg_string*  
 **适用范围**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [当前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658)）。  
  
 是一个字符串括在单引号和包含参数值的占位符。 该错误消息最长可以有 2,047 个字符。 如果该消息包含的字符数等于或超过 2,048 个，则只能显示前 2,044 个并添加一个省略号以表示该消息已被截断。 请注意，由于内部存储行为的缘故，代替参数使用的字符数比输出所显示的字符数要多。  有关消息字符串的结构和用法的字符串中的参数的信息，请参阅说明*msg_str*中的参数[RAISERROR &#40;Transact SQL &#41;](../../t-sql/language-elements/raiserror-transact-sql.md).  
  
 *param_value*  
 在消息中使用的参数值。 可以是多个参数值。 值的顺序必须与占位符变量在消息中出现的次序相同。 值的最大数目为 20。  
  
## <a name="return-types"></a>返回类型  
 **nvarchar**  
  
## <a name="remarks"></a>注释  
 与 RAISERROR 语句相似，FORMATMESSAGE 用提供的参数值替换消息中的占位符变量来编辑消息。 有关错误消息并编辑过程中允许的占位符的详细信息，请参阅[RAISERROR &#40;Transact SQL &#41;](../../t-sql/language-elements/raiserror-transact-sql.md).  
  
 FORMATMESSAGE 查找使用用户当前语言的消息。 如果消息没有本地化版本，则使用美国英语版本。  
  
 对于本地化的消息，提供的参数值必须与美国英语版本中的参数占位符对应。 也就是说，本地化版本的参数 1 必须对应于美国英语版本的参数 1，本地化版本的参数 2 必须对应于美国英语版本的参数 2，依此类推。  
  
## <a name="examples"></a>示例  
  
### <a name="a-example-with-a-message-number"></a>A. 与大量消息的示例  
 下面的示例使用复制邮件`20009`存储在 sys.messages 作为中，"%s 可能未将项目添加到发布 '%s'。"FORMATMESSAGE 将为参数占位符替换值 `First Variable` 和 `Second Variable`。 生成的字符串中，"项目第一个变量无法不添加到发布第二个变量。"，存储在本地变量`@var1`。  
  
```  
SELECT text FROM sys.messages WHERE message_id = 20009 AND language_id = 1033;  
DECLARE @var1 VARCHAR(200);   
SELECT @var1 = FORMATMESSAGE(20009, 'First Variable', 'Second Variable');   
SELECT @var1;  
```  
  
### <a name="b-example-with-a-message-string"></a>B. 使用的消息字符串的示例  
  
**适用范围**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [当前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658)）。  
  
 下面的示例接受的字符串作为输入。  
  
```  
SELECT FORMATMESSAGE('This is the %s and this is the %s.', 'first variable', 'second variable') AS Result;  
```  
  
 返回：`This is the first variable and this is the second variable.`  
  
### <a name="c-additional-message-string-formatting-examples"></a>C. 其他消息字符串设置格式示例  
 下面的示例演示了各种的格式设置选项。  
  
```  
SELECT FORMATMESSAGE('Signed int %i, %d %i, %d, %+i, %+d, %+i, %+d', 5, -5, 50, -50, -11, -11, 11, 11);  
SELECT FORMATMESSAGE('Signed int with leading zero %020i', 5);  
SELECT FORMATMESSAGE('Signed int with leading zero 0 %020i', -55);  
SELECT FORMATMESSAGE('Unsigned int %u, %u', 50, -50);  
SELECT FORMATMESSAGE('Unsigned octal %o, %o', 50, -50);  
SELECT FORMATMESSAGE('Unsigned hexadecimal %x, %X, %X, %X, %x', 11, 11, -11, 50, -50);  
SELECT FORMATMESSAGE('Unsigned octal with prefix: %#o, %#o', 50, -50);  
SELECT FORMATMESSAGE('Unsigned hexadecimal with prefix: %#x, %#X, %#X, %X, %x', 11, 11, -11, 50, -50);  
SELECT FORMATMESSAGE('Hello %s!', 'TEST');  
SELECT FORMATMESSAGE('Hello %20s!', 'TEST');  
SELECT FORMATMESSAGE('Hello %-20s!', 'TEST');  
SELECT FORMATMESSAGE('Hello %20s!', 'TEST');  
```  
  
## <a name="see-also"></a>另请参阅  
 [THROW &#40;Transact SQL &#41;](../../t-sql/language-elements/throw-transact-sql.md)   
 [sp_addmessage &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md)   
 [sys.messages (Transact-SQL)](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [System Functions (Transact-SQL)](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [RAISERROR &#40;Transact SQL &#41;](../../t-sql/language-elements/raiserror-transact-sql.md)  
  
  

