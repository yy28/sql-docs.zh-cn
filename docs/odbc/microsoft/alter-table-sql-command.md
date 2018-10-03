---
title: ALTER TABLE-SQL 命令 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- alter table [ODBC]
ms.assetid: 3a01a291-f4d9-43bc-a725-5a95546ff364
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 054cc0f649a120805fb3ed2f5f58911959ddceaf
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47694746"
---
# <a name="alter-table---sql-command"></a>ALTER TABLE - SQL 命令
以编程方式修改的表的结构。  
  
## <a name="syntax"></a>语法  
  
```  
  
ALTER TABLE TableName1  
   ADD | ALTER [COLUMN] FieldName1  
      FieldType [(nFieldWidth [, nPrecision])]  
      [NULL | NOT NULL]  
      [CHECK lExpression1 [ERROR cMessageText1]]  
      [DEFAULT eExpression1]  
      [PRIMARY KEY | UNIQUE]  
      [REFERENCES TableName2 [TAG TagName1]]  
      [NOCPTRANS]  
 - Or -  
ALTER TABLE TableName1  
   ALTER [COLUMN] FieldName2  
      [NULL | NOT NULL]  
      [SET DEFAULT eExpression2]  
      [SET CHECK lExpression2 [ERROR cMessageText2]]  
      [DROP DEFAULT]  
      [DROP CHECK]  
 - Or -  
ALTER TABLE TableName1  
   [DROP [COLUMN] FieldName3]  
   [SET CHECK lExpression3 [ERROR cMessageText3]]  
   [DROP CHECK]  
   [ADD PRIMARY KEY eExpression3 TAG TagName2]  
   [DROP PRIMARY KEY]  
   [ADD UNIQUE eExpression4 [TAG TagName3]]  
   [DROP UNIQUE TAG TagName4]  
   [ADD FOREIGN KEY [eExpression5] TAG TagName4  
      REFERENCES TableName2 [TAG TagName5]]  
   [DROP FOREIGN KEY TAG TagName6 [SAVE]]  
   [RENAME COLUMN FieldName4 TO FieldName5]  
   [NOVALIDATE]  
```  
  
## <a name="arguments"></a>参数  
 *TableName1*  
 指定修改其结构的表的名称。  
  
 添加 [COLUMN] *FieldName1*  
 指定要添加的字段的名称。  
  
 ALTER [COLUMN] *FieldName1*  
 指定要修改现有字段的名称。  
  
 *FieldType* [( *nFieldWidth* [， *nPrecision*]])  
 为新的或修改字段中指定的字段类型、 字段宽度和字段精度 （数字的小数位数）。  
  
 *FieldType*是指示该字段的一个单一字母[数据类型](../../odbc/microsoft/visual-foxpro-field-data-types.md)。 某些字段数据类型需要您指定*nFieldWidth*或*nPrecision*和 / 或。  
  
 *nFieldWidth*并*nPrecision*忽略 D、 G、 我、 L、 M、 P、 T 和 Y 的类型。 默认情况下*nPrecision*为零 （没有小数位），如果*nPrecision*则不包含 B、 F 或 N 类型。  
  
 NULL &#124; NOT NULL  
 允许或阻止的字段中的 null 值。  
  
 如果省略 NULL 和 NOT NULL，NULL 设置的当前设置确定字段中是否允许 null 值。 但是，如果你省略 NULL 和 NOT NULL 并且包括在主键或唯一的子句，忽略 SET NULL 的当前设置，该字段不是默认情况下为 NULL。  
  
 检查*lExpression1*  
 指定字段的验证规则。 *lExpression1*必须计算为逻辑表达式，而且可以是用户定义函数或存储的过程。 只要附加一个空记录，检查验证规则。 如果验证规则不允许空字段值在追加的记录中，将生成错误。  
  
 错误*cMessageText1*  
 指定当字段验证规则将生成错误时显示错误消息。  
  
 默认*eExpression1*  
 指定字段的默认值。 数据类型*eExpression1*必须为该字段的数据类型相同。  
  
 PRIMARY KEY  
 创建主索引标记。 索引标记与该字段具有相同的名称。  
  
 UNIQUE  
 创建具有相同名称的字段的候选索引标记。  
  
> [!NOTE]  
>  候选索引 （包括用于 ALTER TABLE 或 CREATE TABLE 中的 ANSI 兼容性的唯一选项创建） 不同于创建索引命令中使用的唯一选项的索引。 创建索引命令中使用 UNIQUE 索引允许重复的索引键;候选索引不允许有重复的索引键。  
  
 在主键或候选索引使用的字段中不允许 null 值和重复的记录。  
  
 如果使用添加列创建一个新字段，Visual FoxPro 将不会生成错误，如果创建主键或候选索引支持 null 值的字段。 但是，Visual FoxPro 将生成错误，如果你尝试使用主键或候选索引的字段中输入空值或重复值。  
  
 如果您正在修改现有字段，并且或者候选索引表达式组成的表中的字段，Visual FoxPro 会检查以查看它们是否包含 null 值或重复的记录的字段。 如果是这样，Visual FoxPro 生成错误，并不更改表。  
  
 引用*TableName2*标记*TagName1*  
 指定与之建立持久关系的父表。 标记*TagName1*指定关系所基于的父表的索引标记。 索引的标记名称可包含最多 10 个字符。  
  
 NOCPTRANS  
 可以防止转换到字符和备注字段的不同代码页。 如果表转换为另一个代码页，将不转换为其指定 NOCPTRANS 的字段。 可以仅为字符和备注字段指定 NOCPTRANS。  
  
 以下示例创建名为 mytable，其中包含两个字符字段和两个备注字段的表。 第二个字符字段、 char2 和第二个备注字段，memo2，包括 NOCPTRANS 以防止转换。  
  
```  
CREATE TABLE mytable (char1 C(10), char2 C(10) NOCPTRANS,;  
   memo1 M, memo2 M NOCPTRANS)  
```  
  
 ALTER [COLUMN] *FieldName2*  
 指定要修改现有字段的名称。  
  
 设置默认值*eExpression2*  
 指定现有字段的新默认值。 数据类型*eExpression2*必须为该字段的数据类型相同。  
  
 集检查*lExpression2*  
 指定的新的验证规则的现有字段。 *lExpression2*计算结果必须为逻辑表达式，可能是用户定义函数或存储的过程。  
  
 错误*cMessageText2*  
 指定当字段验证规则将生成错误时显示错误消息。 仅当浏览或编辑窗口中更改数据时，会显示消息。  
  
 DROP DEFAULT  
 删除现有字段的默认值。  
  
 删除检查  
 删除现有字段的验证规则。  
  
 拖放 [COLUMN] *FieldName3*  
 指定要从表中删除的字段。 从表中删除字段还会删除该字段的默认值设置和字段验证规则。  
  
 如果索引键或触发器表达式引用该字段，这些表达式无效时将删除的字段。 在这种情况下，将删除的字段但无效索引键或触发器表达式将在运行时生成错误时将不会生成错误。  
  
 集检查*lExpression3*  
 指定表验证规则。 *lExpression3*计算结果必须为逻辑表达式，可能是用户定义函数或存储的过程。  
  
 错误*cMessageText3*  
 指定的错误消息显示时表验证规则将生成错误。 仅当浏览或编辑窗口中更改数据时，会显示消息。  
  
 删除检查  
 删除表的验证规则。  
  
 添加主键*eExpression3*标记*TagName2*  
 向表中添加主索引。 *eExpression3*指定主索引键表达式，并*TagName2*指定主索引标记的名称。 索引的标记名称可包含最多 10 个字符。 如果标记*TagName2*省略和*eExpression3*是单个字段中，主索引标记中指定的字段作为具有相同的名称*eExpression3*。  
  
 删除主键  
 删除主索引和相应索引的标记。 因为一个表只能有一个主键，不需要指定为主键的名称。 删除主索引也会删除任何基于主键的永久关系。  
  
 添加 UNIQUE *eExpression4*[标记*TagName3*]  
 向表中添加一个候选项的索引。 *eExpression4*指定候选索引键的表达式，并*TagName3*指定候选索引标记的名称。 索引的标记名称可包含最多 10 个字符。 如果省略标记*TagName3* ; 如果*eExpression4*是单个字段，候选索引标记中指定的字段作为具有相同的名称*eExpression4*。  
  
 删除唯一标记*TagName4*  
 删除候选索引和相应索引的标记。 因为一个表可以包含多个候选键，必须指定候选索引标记的名称。  
  
 添加外键 [ *eExpression5*] 标记*TagName4*  
 向表中添加外 （非主键） 索引。 *eExpression5*指定外索引键表达式，并*TagName4*指定外索引标记的名称。 索引的标记名称可包含最多 10 个字符。  
  
 引用*TableName2*[标记*TagName5*]  
 指定与之建立持久关系的父表。 包含标记*TagName5*建立基于现有索引标记为父表的关系。 索引的标记名称可包含最多 10 个字符。 如果省略标记*TagName5*，使用父表的主索引标记建立关系。  
  
 删除外键标记*TagName6*[保存]  
 删除其索引标记是外键*TagName6*。 如果省略保存，从结构化索引中删除索引标记。 包含保存防止删除从结构化索引的索引标记。  
  
 重命名列*FieldName4*TO *FieldName5*  
 可以更改表中字段的名称。 *FieldName4*指定重命名字段的名称。 *FieldName5*指定字段的新名称。  
  
> [!CAUTION]  
>  重命名表的字段，因为索引表达式、 字段和表验证规则、 命令和函数可能引用原始字段名称时应格外小心。  
  
 NOVALIDATE  
 指定 Visual FoxPro 允许要对表; 的结构进行更改这些更改可能会违反表中的数据的完整性。 默认情况下，Visual FoxPro 阻止进行更改违反的表中的数据完整性的 ALTER TABLE。 包括 NOVALIDATE 重写此默认行为。  
  
## <a name="remarks"></a>备注  
 ALTER TABLE 可以用于修改尚未添加到数据库的表的结构。 但是，如果包括默认、 外键、 主键、 引用，或修改可用的表时设置子句 Visual FoxPro 将生成错误。  
  
 ALTER TABLE 可能会重新生成表创建一个新的表头和将记录追加到表标头。 例如，更改字段的类型或宽度，这种情况可能会导致要重新生成的表。  
  
 重新生成表后，字段验证规则执行的任何更改其类型或宽度的字段。 如果更改类型或表中的任何字段的宽度，则执行表规则。  
  
 如果修改字段或表的表的已记录的验证规则，Visual FoxPro 测试对现有数据的新字段或表验证规则，并发出上第一个匹配项的字段或表的验证规则或触发器冲突的警告。  
  
 如果您修改的表是在数据库中，ALTER TABLE-SQL 需要独占使用的数据库。 若要打开用于独占使用的数据库，请打开数据库中包括排他。  
  
## <a name="see-also"></a>请参阅  
 [CREATE TABLE-SQL 命令](../../odbc/microsoft/create-table-sql-command.md)   
 [INDEX 命令](../../odbc/microsoft/index-command.md)
