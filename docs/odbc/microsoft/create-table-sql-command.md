---
title: CREATE TABLE-SQL 命令 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- CREATE TABLE [ODBC]
ms.assetid: be2143ba-fc16-42c9-84f7-8985cd924860
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2f979ccb5a44ada8e86424e0f6134f39d28a021d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68096604"
---
# <a name="create-table---sql-command"></a>CREATE TABLE - SQL 命令
创建某个表具有指定的字段。  
  
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
 CREATE TABLE &#124; DBF *TableName1*  
 指定要创建的表的名称。 表和 DBF 选项是相同的。  
  
 名称*LongTableName*  
 指定表的长名称。 仅当数据库已打开，因为长表名存储在数据库中时，可以指定一个长表名。  
  
 长名称可包含最多 128 个字符，并且可以用它来替换在数据库中的短文件名。  
  
 FREE  
 指定表将不添加到打开的数据库。 免费版不是必需的如果数据库未打开。  
  
 *(FieldName1 FieldType* [( *nFieldWidth* [, *nPrecision*])]  
 指定字段名称、 字段类型、 字段宽度和字段精度 （数字的小数位数），分别。  
  
 *FieldType*是，该值指示该字段的一个单一字母[数据类型](../../odbc/microsoft/visual-foxpro-field-data-types.md)。 某些字段数据类型需要您指定*nFieldWidth*或*nPrecision*和 / 或。  
  
 *nFieldWidth*并*nPrecision*忽略 D、 G、 我、 L、 M、 P、 T 和 Y 的类型。 *nPrecision*默认为零 （没有小数位），如果*nPrecision*不包括 B、 F 或 N 类型。  
  
 NULL  
 允许 null 值的字段中。  
  
 NOT NULL  
 阻止的字段中的 null 值。  
  
 如果省略 NULL 和 NOT NULL，NULL 设置的当前设置确定字段中是否允许 null 值。 但是，如果你省略 NULL 和 NOT NULL 并且包括在主键或唯一的子句，忽略 SET NULL 的当前设置，该字段的默认值为 NOT NULL。  
  
 检查*lExpression1*  
 指定字段的验证规则。 *lExpression1*可以是用户定义函数。 只要附加一个空记录，检查验证规则。 如果验证规则不允许空字段值在追加的记录中，将生成错误。  
  
 错误*cMessageText1*  
 指定当字段规则将生成错误时，Visual FoxPro 显示的错误消息。 在浏览窗口或编辑窗口中更改数据时才会显示消息。  
  
 默认*eExpression1*  
 指定字段的默认值。 数据类型*eExpression1*必须是字段的数据类型相同。  
  
 PRIMARY KEY  
 创建主索引的字段。 主索引标记与该字段具有相同的名称。  
  
 UNIQUE  
 创建候选索引的字段。 候选索引标记与该字段具有相同的名称。  
  
> [!NOTE]  
>  候选项 （通过在 CREATE TABLE 或 ALTER TABLE-SQL 中包含的独特选项创建） 的索引不是使用索引命令中的唯一选项创建的索引相同。 使用索引命令中的唯一选项创建的索引允许重复的索引键;候选索引不允许有重复的索引键。 请参阅[索引](../../odbc/microsoft/index-command.md)为其唯一的选项的其他信息。  
  
 在主键或候选索引使用的字段中不允许 null 值和重复的记录。 但是，Visual FoxPro 将不生成错误，如果创建主键或候选索引支持 null 值的字段。 Visual FoxPro 将生成错误，如果你尝试使用主键或候选索引的字段中输入空值或重复值。  
  
 引用*TableName2*[标记*TagName1*]  
 指定与之建立持久关系的父表。 如果省略标记*TagName1*，使用父表的主索引键建立关系。 如果父表不具有主索引，Visual FoxPro 将生成错误。  
  
 包含标记*TagName1*建立基于现有索引标记为父表的关系。 索引的标记名称可包含最多 10 个字符。  
  
 父表不能为免费的表。  
  
 NOCPTRANS  
 可以防止转换到字符和备注字段的不同代码页。 如果表转换为另一个代码页，将不转换为其指定 NOCPTRANS 的字段。 可以仅为字符和备注字段指定 NOCPTRANS。  
  
 以下示例创建名为 mytable 包含两个字符字段和两个备注字段的表。 第二个字符字段、 char2 和第二个备注字段，memo2，包括 NOCPTRANS 以防止转换。  
  
```  
CREATE TABLE mytable (char1 C(10), char2 C(10) NOCPTRANS,;  
   memo1 M, memo2 M NOCPTRANS)  
```  
  
 主键*eExpression2*标记*TagName2*  
 指定要创建主索引。 *eExpression2*指定表中的任何字段的组合。 标记*TagName2*指定创建的主索引标记的名称。 索引的标记名称可包含最多 10 个字符。  
  
 因为一个表可以包含一个主索引，不能包含此子句，如果你已创建主索引的字段。 Visual FoxPro 生成错误，如果在 CREATE TABLE 中包括多个 PRIMARY KEY 子句。  
  
 唯一*eExpression3*标记*TagName3*  
 创建一个候选项的索引。 *eExpression3*指定表中的任何字段的组合。 但是，如果您使用 PRIMARY KEY 选项之一创建了主索引，不能包含指定的主索引的字段。 标记*TagName3*指定创建的候选索引标记的标记名称。 索引的标记名称可包含最多 10 个字符。  
  
 一个表可以有多个候选项索引。  
  
 外键*eExpression4*标记*TagName4*[NODUP]  
 创建外 （非主键） 索引并建立与父表的关系。 *eExpression4*指定外索引键表达式，并*TagName4*指定创建的索引外键标记的名称。 索引的标记名称可包含最多 10 个字符。 包括 NODUP 创建候选外索引。  
  
 您可以创建多个外的索引对于表，但外索引表达式必须指定表中的不同字段。  
  
 引用*TableName3*[标记*TagName5*]  
 指定与之建立持久关系的父表。 包含标记*TagName5*建立基于父表的索引标记的关系。 索引的标记名称可包含最多 10 个字符。 默认情况下，如果省略标记*TagName5，* 使用父表的主索引键建立关系。  
  
 检查*eExpression2*[错误*cMessageText2*]  
 指定表验证规则。 错误*cMessageText2*指定 Visual FoxPro 表验证规则执行时将显示错误消息。 仅当数据在一个浏览窗口内已更改，或编辑窗口时，会显示消息。  
  
 从数组*ArrayName*  
 指定一个现有数组，其内容是名称、 类型、 精度和小数位数为表中每个字段的名称。 可以使用定义数组的内容**AFIELDS**（） 函数。  
  
## <a name="remarks"></a>备注  
 新表中的最低可用工作区打开，可访问的别名。 以独占方式，打开是新表，而不考虑设置排他的当前设置。  
  
 如果数据库处于打开状态，并且不包含免费的子句，新表添加到数据库。 不能使用与数据库中的表相同的名称来创建新表。  
  
 如果数据库处于打开状态，CREATE TABLE-SQL 需要独占使用的数据库。 若要打开用于独占使用的数据库，请打开数据库中包括排他。  
  
 如果创建新表时，数据库未打开，包括名称、 检查、 默认、 外键、 主键或引用子句将生成错误。  
  
> [!NOTE]  
>  CREATE TABLE 语法使用逗号来分隔某些 CREATE TABLE 选项。 此外，NULL、 不为 NULL、 检查、 默认、 PRIMARY KEY 和唯一的子句必须放在括号中包含的列定义。  
  
## <a name="driver-remarks"></a>驱动程序备注  
 当你的应用程序发送的 ODBC SQL 语句时创建表与数据源，Visual FoxPro ODBC 驱动程序转换为该命令使用下表中所示的语法的 Visual FoxProCREATE TABLE 命令。  
  
|ODBC 语法|Visual FoxPro 语法|  
|-----------------|--------------------------|  
|CREATE TABLE*基础表名称*<br /><br /> (*列标识符的数据类型*<br /><br /> [不为 NULL]<br /><br /> [，*列标识符的数据类型*<br /><br /> [NOT NULL]...)|创建表*TableName1* [名称*LongTableName*]<br /><br /> (*FieldName1* *FieldType*<br /><br /> [(*nFieldWidth* [, *nPrecision*])]<br /><br /> [不为 NULL])|  
  
 创建时使用的驱动程序的表，该驱动程序以允许访问由其他用户表的创建后立即关闭表。 这不同于 Visual FoxPro，让表保留在创建时以独占方式打开。 但是，如果数据源包含 CREATE TABLE 语句上的存储的过程执行，表处于打开状态。  
  
 如果数据源是数据库 （.dbc 文件），Visual FoxPro ODBC 驱动程序将创建一个名为表*LongTableName*与同名*基础表名称*。  
  
### <a name="using-data-definition-language-ddl"></a>使用数据定义语言 (DDL)  
 在以下位置中，不能包含 DDL:  
  
-   批处理 SQL 语句中，需要使用事务  
  
-   在手动提交模式下，需要事务，除非你的应用程序首先调用语句后面**SQLTransact**。  
  
 例如，如果你想要创建一个临时表，应在开始需要事务的语句之前创建的表。 如果在一批需要事务的 SQL 语句包括 CREATE TABLE 语句，该驱动程序将返回一条错误消息。  
  
## <a name="see-also"></a>请参阅  
 [ALTER TABLE-SQL 命令](../../odbc/microsoft/alter-table-sql-command.md)   
 [支持的数据类型 （Visual FoxPro ODBC 驱动程序）](../../odbc/microsoft/supported-data-types-visual-foxpro-odbc-driver.md)   
 [INSERT-SQL 命令](../../odbc/microsoft/insert-sql-command.md)   
 [SELECT - SQL 命令](../../odbc/microsoft/select-sql-command.md)
