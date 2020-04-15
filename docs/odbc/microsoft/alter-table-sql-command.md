---
title: 更改表 - SQL 命令 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 587d721522503f9b392bb8be7433850fd7449efb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304708"
---
# <a name="alter-table---sql-command"></a>ALTER TABLE - SQL 命令
以编程方式修改表的结构。  
  
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
 *表名称1*  
 指定其结构被修改的表的名称。  
  
 添加 [COLUMN]*字段名称1*  
 指定要添加的字段的名称。  
  
 更改 [COLUMN]*字段名称1*  
 指定要修改的现有字段的名称。  
  
 *字段类型* *[（n字段宽度* *[，n 精度*]）  
 指定新字段或修改字段的字段类型、字段宽度和字段精度（小数位数）。  
  
 *字段类型*是指示字段[数据类型](../../odbc/microsoft/visual-foxpro-field-data-types.md)的单个字母。 某些字段数据类型要求您指定*nFieldWidth*或*nPrecision*或两者。  
  
 *nFieldWidth*和*nPrecision*被忽略 D、G、I、L、M、P、T 和 Y 类型。 默认情况下，如果 B、F 或 N 类型不包括*nPrecision，**则 nPrecision*为零（无小数位数）。  
  
 NULL &#124; NOT NULL  
 允许或阻止字段中的空值。  
  
 如果省略 NULL 和 NOT NULL，则"设置 NULL"的当前设置将确定字段中是否允许空值。 但是，如果省略 NULL 和 NOT NULL 并包含"主密钥"或"独立"子句，则将忽略 SET NULL 的当前设置，默认情况下该字段不是 NULL。  
  
 CHECK *lExpression1*  
 指定字段的验证规则。 *lExpression1*必须计算到逻辑表达式，并且可以是用户定义的函数或存储过程。 每当追加空白记录时，都会检查验证规则。 如果验证规则不允许追加记录中的空白字段值，则生成错误。  
  
 错误*cMessage文本1*  
 指定字段验证规则生成错误时显示的错误消息。  
  
 DEFAULT *eExpression1*  
 指定字段的默认值。 *eExpression1*的数据类型必须与字段的数据类型相同。  
  
 PRIMARY KEY  
 创建主索引标记。 索引标记的名称与字段相同。  
  
 UNIQUE  
 创建与字段同名的候选索引标记。  
  
> [!NOTE]  
>  候选索引（通过包含"唯一"选项（在 ALTER TABLE 或 CREATE TABLE 中提供 ANSI 兼容性）与在 INDEX 命令中使用"唯一"选项创建的索引不同。 在 INDEX 命令中使用 UNIQUE 创建的索引允许重复索引键;候选索引不允许重复的索引键。  
  
 对于用于主索引或候选索引的字段，不允许使用空值和重复记录。  
  
 如果使用 ADD COLUMN 创建新字段，则如果为支持空值的字段创建主索引或候选索引，Visual FoxPro 将不会生成错误。 但是，如果您尝试在用于主索引或候选索引的字段中输入空值或重复值，则 Visual FoxPro 将生成错误。  
  
 如果要修改现有字段，并且主索引表达式由表中的字段组成，Visual FoxPro 将检查字段以查看这些字段是否包含空值或重复记录。 如果这样做，Visual FoxPro 将生成错误，并且表不会更改。  
  
 参考*表名称2* *标签名称1*  
 指定建立持久关系的父表。 TAG *TagName1*指定关系所基于的父表的索引标记。 索引标记名称最多可以包含 10 个字符。  
  
 NOCPTRANS  
 防止将字符和备忘录字段翻译成其他代码页。 如果表转换为另一个代码页，则不会转换指定 NOCPTRANS 的字段。 NOCPTRANS 只能为字符和备忘录字段指定。  
  
 下面的示例创建一个名为 mytable 的表，其中包含两个字符字段和两个备忘录字段。 第二个字符字段 char2 和第二个备忘录字段备忘录 2 包括 NOCPTRANS 以防止翻译。  
  
```  
CREATE TABLE mytable (char1 C(10), char2 C(10) NOCPTRANS,;  
   memo1 M, memo2 M NOCPTRANS)  
```  
  
 更改 [COLUMN]*字段名称2*  
 指定要修改的现有字段的名称。  
  
 设置默认*e 表达式2*  
 为现有字段指定新的默认值。 *eExpression2*的数据类型必须与字段的数据类型相同。  
  
 设置 CHECK *l 表达式2*  
 为现有字段指定新的验证规则。 *lExpression2*必须计算到逻辑表达式，并且可能是用户定义的函数或存储过程。  
  
 错误*cMessage文本2*  
 指定字段验证规则生成错误时显示的错误消息。 仅当在"浏览"或"编辑"窗口中更改数据时，才会显示该消息。  
  
 DROP DEFAULT  
 删除现有字段的默认值。  
  
 掉落检查  
 删除现有字段的验证规则。  
  
 DROP [列）*字段名称3*  
 指定要从表中删除的字段。 从表中删除字段还会删除字段的默认值设置和字段验证规则。  
  
 如果索引键或触发器表达式引用该字段，则删除该字段时，表达式将变为无效。 在这种情况下，删除字段时不会生成错误，但无效的索引键或触发器表达式将在运行时生成错误。  
  
 设置 CHECK *l 表达式3*  
 指定表验证规则。 *lExpression3*必须计算到逻辑表达式，并且可能是用户定义的函数或存储过程。  
  
 错误*cMessage文本3*  
 指定表验证规则生成错误时显示的错误消息。 仅当在"浏览"或"编辑"窗口中更改数据时，才会显示该消息。  
  
 掉落检查  
 删除表的验证规则。  
  
 添加主键*eExpression3*标签*标签名称2*  
 向表添加主索引。 *eExpression3*指定主索引键表达式 *，TagName2*指定主索引标记的名称。 索引标记名称最多可以包含 10 个字符。 如果省略*了 TAG TagName2，* 并且*eExpression3*是单个字段，则主索引标记的名称与*eExpression3*中指定的字段的名称相同。  
  
 删除主键  
 删除主索引及其索引标记。 由于表只能有一个主键，因此不必指定主键的名称。 删除主索引还会删除基于主键的任何持久关系。  
  
 添加独立*电子表达式4* *[TAG 标签名称3*]  
 向表添加候选索引。 *eExpression4*指定候选索引键表达式 *，TagName3*指定候选索引标记的名称。 索引标记名称最多可以包含 10 个字符。 如果省略 TAG *TagName3，* 并且*eExpression4*是单个字段，则候选索引标记的名称与*eExpression4*中指定的字段的名称相同。  
  
 删除唯一*标签名称4*  
 删除候选索引及其索引标记。 由于表可以有多个候选键，因此必须指定候选索引标记的名称。  
  
 添加外键 = *eExpression5*[TAG*标签名称4*  
 向表添加外来（非主）索引。 *eExpression5*指定外索引键表达式 *，TagName4*指定外索引标记的名称。 索引标记名称最多可以包含 10 个字符。  
  
 参考*表名称2*[TAG*标签名称5*]  
 指定建立持久关系的父表。 包括 TAG *TagName5，* 以基于父表的现有索引标记建立关系。 索引标记名称最多可以包含 10 个字符。 如果省略 TAG *TagName5，* 则使用父表的主索引标记建立关系。  
  
 删除外国键*标签名称6*[保存]  
 删除索引标记为*TagName6*的外键。 如果省略 SAVE，索引标记将从结构索引中删除。 包括 SAVE 以防止从结构索引中删除索引标记。  
  
 重命名列列*字段名称4*到*字段名称5*  
 允许您更改表中字段的名称。 *FieldName4*指定重命名的字段的名称。 *字段Name5*指定字段的新名称。  
  
> [!CAUTION]  
>  重命名表字段时要小心谨慎，因为索引表达式、字段和表验证规则、命令和函数可能引用原始字段名称。  
  
 无验证  
 指定 Visual FoxPro 允许对表的结构进行更改;这些更改可能会违反表中数据的完整性。 默认情况下，Visual FoxPro 可防止 ALTER TABLE 进行更改，这些更改会违反表中数据的完整性。 包括 NOVALIDATE 以覆盖此默认行为。  
  
## <a name="remarks"></a>备注  
 ALTER TABLE 可用于修改尚未添加到数据库的表的结构。 但是，如果在修改可用表时包含 DEFAULT、外键、主密钥、参考或 SET 子句，则 Visual FoxPro 将生成错误。  
  
 ALTER TABLE 可以通过创建新的表标头并将记录追加到表标头来重建表。 例如，更改字段的类型或宽度可能会导致重建表。  
  
 重建表后，将针对任何类型或宽度更改的字段执行字段验证规则。 如果更改表中任何字段的类型或宽度，则执行表规则。  
  
 如果修改具有记录的表的字段或表验证规则，Visual FoxPro 会针对现有数据测试新的字段或表验证规则，并针对首次出现字段或表验证规则或触发器冲突发出警告。  
  
 如果修改的表位于数据库中，则 ALTER TABLE - SQL 需要独占使用数据库。 要打开数据库供独占使用，请在 OPEN 数据库中包括独占。  
  
## <a name="see-also"></a>另请参阅  
 [创建表 - SQL 命令](../../odbc/microsoft/create-table-sql-command.md)   
 [INDEX 命令](../../odbc/microsoft/index-command.md)
