---
title: 创建表的 SQL 命令 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- CREATE TABLE [ODBC]
ms.assetid: be2143ba-fc16-42c9-84f7-8985cd924860
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 35a23b8c648b5ffbf2a2000c949f1cb097ba91ca
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32905082"
---
# <a name="create-table---sql-command"></a>创建表的 SQL 命令
创建具有指定的字段的表。  
  
 Visual FoxPro ODBC 驱动程序支持本机 Visual FoxPro 语言语法，此命令。 特定于驱动程序的信息，请参阅**驱动程序备注**。  
  
## <a name="syntax"></a>语法  
  
```  
  
CREATE TABLE | DBF TableName1 [NAME LongTableName] [FREE]  
   (FieldName1FieldType [(nFieldWidth [, nPrecision])]  
      [NULL | NOT NULL]   
      [CHECK lExpression1 [ERROR cMessageText1]]  
      [DEFAULT eExpression1]  
      [PRIMARY KEY | UNIQUE]  
      [REFERENCES TableName2 [TAG TagName1]]  
      [NOCPTRANS]  
   [, FieldName2 ...]  
      [, PRIMARY KEY eExpression2 TAG TagName2  
      |, UNIQUE eExpression3 TAG TagName3]  
      [, FOREIGN KEY eExpression4 TAG TagName4 [NODUP]  
            REFERENCES TableName3 [TAG TagName5]]  
      [, CHECK lExpression2 [ERROR cMessageText2]])  
| FROM ARRAY ArrayName  
```  
  
## <a name="arguments"></a>参数  
 创建表&#124;DBF *TableName1*  
 指定要创建的表的名称。 表和 DBF 选项是相同的。  
  
 名称*LongTableName*  
 指定表的长名称。 仅当打开，数据库时由于长表名称存储在数据库，则可以指定长表名称。  
  
 长名称可以包含最多为 128 个字符，并且可用于代替在数据库中的短文件名。  
  
 FREE  
 指定表将不添加到打开的数据库。 免费不是必需的如果数据库未打开。  
  
 *(FieldName1 FieldType* [( *nFieldWidth* [， *nPrecision*])]  
 分别指定字段名、 字段类型、 字段宽度和字段精度 （的小数位数的数字）。  
  
 *FieldType* ，该值指示该字段是一个字母[数据类型](../../odbc/microsoft/visual-foxpro-field-data-types.md)。 某些字段数据类型均要求您指定*nFieldWidth*或*nPrecision*和/或文件名。  
  
 *nFieldWidth*和*nPrecision* D、 G、 I、 L、 M、 P、 T、 和 Y 为忽略类型。 *nPrecision*默认为零 （没有小数位），如果*nPrecision*不包含 B、 F 或 N 类型。  
  
 NULL  
 允许的字段中的 null 值。  
  
 NOT NULL  
 阻止的字段中的 null 值。  
  
 如果你省略 NULL，而不为 NULL，设置为 NULL 的当前设置将确定在字段中是否允许空值。 但是，如果你省略 NULL 和 NOT NULL，并且包括主键或唯一子句，忽略设置为 NULL 的当前设置，该字段默认为 NOT NULL。  
  
 检查*lExpression1*  
 指定字段的验证规则。 *lExpression1*可以是用户定义函数。 只要附加一个空记录，则会检查验证规则。 如果验证规则不允许为空白字段值为追加的记录中，将生成错误。  
  
 错误*cMessageText1*  
 指定 Visual FoxPro 显示字段规则将生成错误时的错误消息。 仅当数据更改一个浏览窗口或编辑窗口中时，将显示消息。  
  
 默认*eExpression1*  
 指定字段的默认值。 数据类型*eExpression1*必须是字段的数据类型相同。  
  
 PRIMARY KEY  
 创建一个主索引的字段。 主索引标记字段具有相同的名称。  
  
 UNIQUE  
 创建一个候选索引的字段。 候选索引标记字段具有相同的名称。  
  
> [!NOTE]  
>  候选 （通过在 CREATE TABLE 或 ALTER TABLE-SQL 中包含的唯一选项创建） 的索引不是使用索引命令中的唯一选项创建的索引相同。 使用索引命令中的唯一选项创建的索引允许重复的索引的键;候选索引不允许重复的索引键。 请参阅[索引](../../odbc/microsoft/index-command.md)有关其唯一的选项的其他信息。  
  
 在主键或候选索引使用的字段中不允许 null 值和重复记录。 但是，Visual FoxPro 将不生成错误，如果创建支持 null 值的字段的主键或候选索引。 Visual FoxPro 将生成错误，如果你尝试使用主键或候选索引的字段中输入值为空或重复。  
  
 引用*TableName2*[标记*TagName1*]  
 指定与之建立持久的关系的父表。 如果省略标记*TagName1*，使用父表的主索引键建立关系。 如果父表不具有主索引，则 Visual FoxPro 生成错误。  
  
 包括标记*TagName1*建立基于父表的现有索引标记的关系。 索引标记名称可以包含最多 10 个字符。  
  
 父表不能为免费的表。  
  
 NOCPTRANS  
 阻止的不同代码页的字符和备注字段的平移。 如果表转换为另一个代码页中，将不会转换为其指定 NOCPTRANS 的字段。 可以仅为的字符和备注字段指定 NOCPTRANS。  
  
 下面的示例创建名为 mytable 包含两个字符字段和两个备注字段的表。 第二个的字符字段、 char2 和第二个的备注字段，memo2，包括 NOCPTRANS 以防止翻译。  
  
```  
CREATE TABLE mytable (char1 C(10), char2 C(10) NOCPTRANS,;  
   memo1 M, memo2 M NOCPTRANS)  
```  
  
 主键*eExpression2*标记*TagName2*  
 指定可用于创建的主索引。 *eExpression2*指定表中的任何字段的组合。 标记*TagName2 的*指定创建的主索引标记的名称。 索引标记名称可以包含最多 10 个字符。  
  
 由于表只能有一个主索引，不能包括此子句，如果你已创建了主索引的字段。 Visual FoxPro 生成错误，如果在创建表中包含多个 PRIMARY KEY 子句。  
  
 唯一*eExpression3*标记*TagName3*  
 创建一个候选索引。 *eExpression3*指定表中的任何字段的组合。 但是，如果你已经使用主键选项之一来创建主索引，不能包括主索引为指定的字段。 标记*TagName3 的*指定创建的候选索引标记的标记名称。 索引标记名称可以包含最多 10 个字符。  
  
 一个表可以有多个候选索引。  
  
 外键*eExpression4*标记*TagName4*[NODUP]  
 创建外的 （非主要） 索引，并建立与父表的关系。 *eExpression4*指定外的索引键表达式，和*TagName4*指定的名称创建的外的索引键标记 *。* 索引标记名称可以包含最多 10 个字符。 包括 NODUP 创建候选外索引。  
  
 你可以创建多个外的索引对于表，但外索引表达式必须指定表中的不同字段。  
  
 引用*TableName3*[标记*TagName5*]  
 指定与之建立持久的关系的父表。 包括标记*TagName5*建立基于父表的索引标记的关系。 索引标记名称可以包含最多 10 个字符。 默认情况下，如果省略标记*TagName5，* 使用父表的主索引键建立关系。  
  
 检查*eExpression2*[错误*cMessageText2*]  
 指定的表验证规则。 错误*cMessageText2*指定 Visual FoxPro 显示表验证规则执行时的错误消息。 仅当数据在一个浏览窗口内已更改，或编辑窗口时，将显示消息。  
  
 从数组*ArrayName*  
 指定一个现有数组，其内容是名称、 类型、 精度和小数位数为表中每个字段的名称。 可以使用定义数组的内容**AFIELDS**（） 函数。  
  
## <a name="remarks"></a>注释  
 新的表在最低可用的工作区中打开，并可以通过其别名访问。 以独占方式，打开为新表，而不考虑独占设置的当前设置。  
  
 如果数据库处于打开状态，并且不包含可用子句，新表添加到数据库。 与数据库中表同名，无法创建新表。  
  
 如果数据库处于打开状态，则创建表的 SQL 需要独占使用的数据库。 若要打开以供独占使用的数据库，包括打开的数据库中的独占。  
  
 如果数据库未打开，在您创建新表，包括名称、 检查、 默认、 外键、 PRIMARY KEY 或引用子句生成错误。  
  
> [!NOTE]  
>  CREATE TABLE 语法使用逗号来分隔某些 CREATE TABLE 选项。 此外，NULL、 不 NULL、 检查、 默认、 PRIMARY KEY 和唯一子句必须放置在括号中且包含的列定义。  
  
## <a name="driver-remarks"></a>驱动程序备注  
 当你的应用程序发送的 ODBC SQL 语句创建表添加到数据源，Visual FoxPro ODBC 驱动程序会将命令转换为使用下表中所示的语法 Visual FoxProCREATE TABLE 命令。  
  
|ODBC 语法|Visual FoxPro 语法|  
|-----------------|--------------------------|  
|CREATE TABLE*基本表名称*<br /><br /> (*列标识符数据类型*<br /><br /> [不为 NULL]<br /><br /> [，*列标识符数据类型*<br /><br /> [不为 NULL]...)|创建表*TableName1* [名称*LongTableName*]<br /><br /> (*FieldName1* *FieldType*<br /><br /> [(*nFieldWidth* [， *nPrecision*])]<br /><br /> [不能为 NULL])|  
  
 当你创建表使用驱动程序时，该驱动程序以允许访问其他用户的表在创建后立即关闭表。 这不同于 Visual FoxPro，保持表以独占方式在创建时处于打开状态。 但是，如果数据源包含 CREATE TABLE 语句上的存储的过程执行，表处于打开状态。  
  
 如果数据源是一个数据库 （.dbc 文件），Visual FoxPro ODBC 驱动程序将创建名为的表*LongTableName*与同名*基本表名*。  
  
### <a name="using-data-definition-language-ddl"></a>使用数据定义语言 (DDL)  
 在以下位置中，不能包含 DDL:  
  
-   批处理 SQL 语句中，需要使用事务  
  
-   在手动提交模式下，必需的事务，除非你的应用程序首先调用语句后面**SQLTransact**。  
  
 例如，如果你想要创建一个临时表，你应创建表，开始需要事务的语句之前。 如果你在一批 SQL 语句要求的事务包含 CREATE TABLE 语句，该驱动程序将返回一条错误消息。  
  
## <a name="see-also"></a>另请参阅  
 [更改表的 SQL 命令](../../odbc/microsoft/alter-table-sql-command.md)   
 [支持的数据类型 （Visual FoxPro ODBC 驱动程序）](../../odbc/microsoft/supported-data-types-visual-foxpro-odbc-driver.md)   
 [插入的 SQL 命令](../../odbc/microsoft/insert-sql-command.md)   
 [SELECT - SQL 命令](../../odbc/microsoft/select-sql-command.md)
