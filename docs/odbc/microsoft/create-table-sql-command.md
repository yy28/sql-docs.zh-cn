---
title: 创建表 - SQL 命令 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dfc80a56a021b1bfeda38115e79f7086632900c8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298687"
---
# <a name="create-table---sql-command"></a>CREATE TABLE - SQL 命令
创建具有指定字段的表。  
  
 Visual FoxPro ODBC 驱动程序支持此命令的本机 Visual FoxPro 语言语法。 有关特定于驱动程序的信息，请参阅**驱动程序备注**。  
  
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
 创建表&#124; DBF*表名称1*  
 指定要创建的表的名称。 TABLE 和 DBF 选项相同。  
  
 名称*长表名称*  
 指定表的长名称。 仅当数据库打开时才能指定长表名称，因为长表名称存储在数据库中。  
  
 长名称最多可以包含 128 个字符，并可用于代替数据库中的短文件名。  
  
 FREE  
 指定表不会添加到打开的数据库。 如果数据库未打开，则不是免费的。  
  
 *（字段名称1 字段类型* *[（n字段宽度* *[，n 精度*=）]  
 分别指定字段名称、字段类型、字段宽度和字段精度（小数位数）。  
  
 *字段类型*是指示字段[数据类型](../../odbc/microsoft/visual-foxpro-field-data-types.md)的单个字母。 某些字段数据类型要求您指定*nFieldWidth*或*nPrecision*或两者。  
  
 *nFieldWidth*和*nPrecision*被忽略 D、G、I、L、M、P、T 和 Y 类型。 *nPrecision*默认为零（没有小数位数），如果 B、F 或 N 类型不包括*nPrecision。*  
  
 Null  
 允许字段中的空值。  
  
 NOT NULL  
 防止字段中的空值。  
  
 如果省略 NULL 和 NOT NULL，则"设置 NULL"的当前设置将确定字段中是否允许空值。 但是，如果省略 NULL 和 NOT NULL 并包含"主密钥"或"独立"子句，则将忽略 SET NULL 的当前设置，并且字段默认为"非 NULL"。  
  
 CHECK *lExpression1*  
 指定字段的验证规则。 *lExpression1*可以是用户定义的函数。 每当追加空白记录时，都会检查验证规则。 如果验证规则不允许追加记录中的空白字段值，则生成错误。  
  
 错误*cMessage文本1*  
 指定字段规则生成错误时显示的错误消息"Visual FoxPro"。 仅当在"浏览"窗口或"编辑"窗口中更改数据时，才会显示该消息。  
  
 DEFAULT *eExpression1*  
 指定字段的默认值。 *eExpression1*的数据类型必须与字段的数据类型相同。  
  
 PRIMARY KEY  
 为字段创建主索引。 主索引标记的名称与字段相同。  
  
 UNIQUE  
 为字段创建候选索引。 候选索引标记的名称与字段相同。  
  
> [!NOTE]  
>  候选索引（通过在"创建表"或"更改表 - SQL"中包含"唯一"选项而创建）与 INDEX 命令中使用"唯一"选项创建的索引不同。 使用 INDEX 命令中的"UNIQUE"选项创建的索引允许重复索引键;候选索引不允许重复的索引键。 有关其"独特"选项的其他信息，请参阅[INDEX。](../../odbc/microsoft/index-command.md)  
  
 对于用于主索引或候选索引的字段，不允许使用空值和重复记录。 但是，如果为支持空值的字段创建主索引或候选索引，Visual FoxPro 不会生成错误。 如果您尝试在用于主索引或候选索引的字段中输入空值或重复值，Visual FoxPro 将生成错误。  
  
 参考*表名称2*[TAG*标签名称1*]  
 指定建立持久关系的父表。 如果省略 TAG *TagName1，* 则使用父表的主索引键建立关系。 如果父表没有主索引，则 Visual FoxPro 将生成错误。  
  
 包括 TAG *TagName1，* 以基于父表的现有索引标记建立关系。 索引标记名称最多可以包含 10 个字符。  
  
 父表不能是可用表。  
  
 NOCPTRANS  
 防止将字符和备忘录字段翻译成其他代码页。 如果表转换为另一个代码页，则不会转换指定 NOCPTRANS 的字段。 NOCPTRANS 只能为字符和备忘录字段指定。  
  
 下面的示例创建一个名为 mytable 的表，其中包含两个字符字段和两个备忘录字段。 第二个字符字段 char2 和第二个备忘录字段备忘录 2 包括 NOCPTRANS 以防止翻译。  
  
```  
CREATE TABLE mytable (char1 C(10), char2 C(10) NOCPTRANS,;  
   memo1 M, memo2 M NOCPTRANS)  
```  
  
 主键*eExpression2* *标签标签名称2*  
 指定要创建的主索引。 *eExpression2*指定表中字段的任何字段或组合。 TAG *TagName2*指定所创建的主要索引标记的名称。 索引标记名称最多可以包含 10 个字符。  
  
 由于表只能有一个主索引，因此，如果已为字段创建了主索引，则无法包含此子句。 如果在"创建表"中包含多个主要密钥子句，Visual FoxPro 将生成错误。  
  
 唯*一电子表达式3**标签标签名称3*  
 创建候选索引。 *eExpression3*指定表中字段的任何字段或组合。 但是，如果已创建具有其中一个"主要密钥"选项的主索引，则无法包括为主索引指定的字段。 TAG *TagName3*为创建的候选索引标记指定标记名称。 索引标记名称最多可以包含 10 个字符。  
  
 表可以有多个候选索引。  
  
 外国密钥*eExpression4* *TAG 标签名称4*[NODUP]  
 创建外（非主）索引并建立与父表的关系。 *eExpression4*指定外索引键表达式 *，TagName4*指定所创建的外索引键标记的名称。 索引标记名称最多可以包含 10 个字符。 包括 NODUP 以创建候选的外来索引。  
  
 可以为表创建多个外来索引，但外索引表达式必须在表中指定不同的字段。  
  
 参考*表名称3*[TAG*标签名称5*]  
 指定建立持久关系的父表。 包括 TAG *TagName5*以建立基于父表的索引标记的关系。 索引标记名称最多可以包含 10 个字符。 默认情况下，如果省略*TAG TagName5，* 则使用父表的主索引键建立关系。  
  
 CHECK *eExpression2*[错误*cMessage文本2*]  
 指定表验证规则。 错误*cMessageText2*指定执行表验证规则时显示的错误消息 Visual FoxPro。 仅当在"浏览"窗口或"编辑"窗口中更改数据时，才会显示该消息。  
  
 从*数组数组名称*  
 指定现有数组的名称，其内容为表中每个字段的名称、类型、精度和比例。 数组的内容可以使用**AFIELDS**（ ） 函数进行定义。  
  
## <a name="remarks"></a>备注  
 新表在最低可用工作区中打开，可通过其别名访问。 无论 SET 独占的当前设置如何，新表都是独占打开的。  
  
 如果数据库处于打开状态，并且不包括 FREE 子句，则新表将添加到数据库中。 不能创建与数据库中的表同名的新表。  
  
 如果数据库处于打开状态，则创建表 - SQL 需要独占使用数据库。 要打开数据库供独占使用，请在 OPEN 数据库中包括独占。  
  
 如果在创建新表时数据库未打开，包括名称、检查、DEFAULT、外键、主键或参考子句都会生成错误。  
  
> [!NOTE]  
>  创建表语法使用逗号分隔某些 CREATE TABLE 选项。 此外，NULL、非 NULL、CHECK、DEFAULT、主键和 UNIQUE 子句必须放置在包含列定义的括号内。  
  
## <a name="driver-remarks"></a>驱动程序备注  
 当应用程序将 ODBC SQL 语句 CREATE TABLE 发送到数据源时，Visual FoxPro ODBC 驱动程序使用下表中显示的语法将该命令转换为 Visual FoxProCREATE TABLE 命令。  
  
|ODBC 语法|可视化 FoxPro 语法|  
|-----------------|--------------------------|  
|创建表*基表名称*<br /><br /> （*列标识符数据类型*<br /><br /> [非空]<br /><br /> *，*列标识符数据类型*<br /><br /> [不作空]|创建*表表名称1* [名称*长表名称*]<br /><br /> （*字段名称1* *字段类型*<br /><br /> *[（nFieldWidth* *[，n精度*]]<br /><br /> [非空]）|  
  
 使用驱动程序创建表时，驱动程序在创建后立即关闭该表，以允许其他用户访问该表。 这与 Visual FoxPro 不同，后者仅在创建时打开表。 但是，如果数据源上包含 CREATE TABLE 语句的存储过程执行，则表将保持打开状态。  
  
 如果数据源是数据库 （.dbc 文件），Visual FoxPro ODBC 驱动程序将创建一个名为*LongTableName*的表，其名称与*基表名称*相同。  
  
### <a name="using-data-definition-language-ddl"></a>使用数据定义语言 （DDL）  
 您不能在以下位置包含 DDL：  
  
-   在需要事务的批处理 SQL 语句中  
  
-   在手动提交模式下，在需要事务的语句之后，除非应用程序首先调用**SQLTransact**。  
  
 例如，如果要创建临时表，则应在开始需要事务的语句之前创建该表。 如果在需要事务的批处理 SQL 语句中包含 CREATE TABLE 语句，驱动程序将返回一条错误消息。  
  
## <a name="see-also"></a>另请参阅  
 [更改表 - SQL 命令](../../odbc/microsoft/alter-table-sql-command.md)   
 [支持的数据类型（可视化福克斯 Pro ODBC 驱动程序）](../../odbc/microsoft/supported-data-types-visual-foxpro-odbc-driver.md)   
 [插入 - SQL 命令](../../odbc/microsoft/insert-sql-command.md)   
 [SELECT - SQL 命令](../../odbc/microsoft/select-sql-command.md)
