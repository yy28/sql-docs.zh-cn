---
title: "更改表的 SQL 命令 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- alter table [ODBC]
ms.assetid: 3a01a291-f4d9-43bc-a725-5a95546ff364
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bafb2f2a11b7108d550dae66db0b5d8e158086a3
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="alter-table---sql-command"></a>更改表的 SQL 命令
以编程方式修改一个表结构。  
  
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
 为新的或修改字段中指定的字段类型、 字段宽度和字段精度 （的小数位数）。  
  
 *FieldType*是一个字母，该值指示该字段的[数据类型](../../odbc/microsoft/visual-foxpro-field-data-types.md)。 某些字段数据类型均要求您指定*nFieldWidth*或*nPrecision*和/或文件名。  
  
 *nFieldWidth*和*nPrecision* D、 G、 I、 L、 M、 P、 T、 和 Y 为忽略类型。 默认情况下， *nPrecision*是零 （没有小数位），如果*nPrecision*不包含 B、 F 或 N 类型。  
  
 NULL &#124;不为 NULL  
 允许或阻止的字段中的 null 值。  
  
 如果你省略 NULL，而不为 NULL，设置为 NULL 的当前设置将确定在字段中是否允许空值。 但是，如果你省略 NULL 和 NOT NULL，并且包括主键或唯一子句，忽略设置为 NULL 的当前设置，该字段不是默认情况下为 NULL。  
  
 检查*lExpression1*  
 指定字段的验证规则。 *lExpression1*计算结果必须为逻辑表达式，可以为用户定义函数或存储的过程。 只要附加一个空记录，则会检查验证规则。 如果验证规则不允许为空白字段值为追加的记录中，将生成错误。  
  
 错误*cMessageText1*  
 指定字段验证规则将生成错误时，将显示错误消息。  
  
 默认*eExpression1*  
 指定字段的默认值。 数据类型*eExpression1*必须是字段的数据类型相同。  
  
 PRIMARY KEY  
 创建一个主索引标记。 索引标记字段具有相同的名称。  
  
 UNIQUE  
 创建具有相同名称的字段的候选索引标记。  
  
> [!NOTE]  
>  候选 （由包括提供针对在 ALTER TABLE 或 CREATE TABLE 中的 ANSI 兼容性的唯一选项创建） 的索引与索引命令中使用唯一的选项创建的索引不同。 创建索引命令中使用 UNIQUE 索引允许重复的索引的键;候选索引不允许重复的索引键。  
  
 在主键或候选索引使用的字段中不允许 null 值和重复记录。  
  
 如果要通过使用添加列来创建新字段，Visual FoxPro 将不会生成错误，如果创建支持 null 值的字段的主键或候选索引。 但是，Visual FoxPro 将生成错误，如果你尝试使用主键或候选索引在字段中输入值为空或重复。  
  
 如果您正在修改现有字段与主站点或候选索引表达式包含表中的字段，则 Visual FoxPro 检查域后，以查看它们是否包含 null 值或重复的记录。 如果他们这样做，将 Visual FoxPro 生成错误并不会更改表。  
  
 引用*TableName2*标记*TagName1*  
 指定与之建立持久的关系的父表。 标记*TagName1*指定关系所基于的父表的索引标记。 索引标记名称可以包含最多 10 个字符。  
  
 NOCPTRANS  
 阻止的不同代码页的字符和备注字段的平移。 如果表转换为另一个代码页中，将不会转换为其指定 NOCPTRANS 的字段。 可以仅为的字符和备注字段指定 NOCPTRANS。  
  
 下面的示例创建名为 mytable 包含两个字符字段和两个备注字段的表。 第二个的字符字段、 char2 和第二个的备注字段，memo2，包括 NOCPTRANS 以防止翻译。  
  
```  
CREATE TABLE mytable (char1 C(10), char2 C(10) NOCPTRANS,;  
   memo1 M, memo2 M NOCPTRANS)  
```  
  
 ALTER [COLUMN] *FieldName2*  
 指定要修改现有字段的名称。  
  
 设置默认值*eExpression2*  
 指定现有字段的新默认值。 数据类型*eExpression2*必须是字段的数据类型相同。  
  
 集检查*lExpression2*  
 指定现有字段的新验证规则。 *lExpression2*逻辑表达式必须计算，而且可能是用户定义函数或存储的过程。  
  
 错误*cMessageText2*  
 指定字段验证规则将生成错误时，将显示错误消息。 仅当数据更改中的浏览或编辑窗口时，将显示消息。  
  
 DROP DEFAULT  
 删除现有字段的默认值。  
  
 删除检查  
 删除现有字段的验证规则。  
  
 拖放 [COLUMN] *FieldName3*  
 指定要从表中删除的字段。 从表中删除字段还会删除该字段的默认值设置和字段验证规则。  
  
 如果索引键或触发器表达式引用的字段，表达式将失效，移除该字段时。 在这种情况下，删除该字段，但无效的索引键或触发器表达式将在运行时生成错误时将不会生成错误。  
  
 集检查*lExpression3*  
 指定的表验证规则。 *lExpression3*逻辑表达式必须计算，而且可能是用户定义函数或存储的过程。  
  
 错误*cMessageText3*  
 指定的错误消息显示时表验证规则将生成错误。 仅当数据更改中的浏览或编辑窗口时，将显示消息。  
  
 删除检查  
 删除表的验证规则。  
  
 添加主键*eExpression3*标记*TagName2*  
 将主索引添加到表。 *eExpression3*指定主索引键表达式，和*TagName2*指定主索引标记的名称。 索引标记名称可以包含最多 10 个字符。 如果标记*TagName2*省略和*eExpression3*是单个字段中，主索引标记中指定字段具有相同名称*eExpression3*。  
  
 删除主键  
 删除主索引和其索引标记。 因为一个表可以有一个主键，不需要指定为主键的名称。 正在删除的主索引还会删除任何基于主键的持续关系。  
  
 添加唯一*eExpression4*[标记*TagName3*]  
 将候选索引添加到表。 *eExpression4*指定候选索引键表达式和*TagName3*指定候选索引标记的名称。 索引标记名称可以包含最多 10 个字符。 如果省略标记*TagName3*如果*eExpression4*是单个字段，候选索引标记中指定字段具有相同名称*eExpression4*。  
  
 删除唯一标记*TagName4*  
 删除的候选索引和其索引标记。 由于一个表可以有多个候选键，必须指定候选索引标记的名称。  
  
 添加外键 [ *eExpression5*] 标记*TagName4*  
 向表中添加外的 （非主要） 索引。 *eExpression5*指定外的索引键表达式，和*TagName4*指定外索引标记的名称。 索引标记名称可以包含最多 10 个字符。  
  
 引用*TableName2*[标记*TagName5*]  
 指定与之建立持久的关系的父表。 包括标记*TagName5*建立基于父表的现有索引标记的关系。 索引标记名称可以包含最多 10 个字符。 如果省略标记*TagName5*，使用父表的主索引标记建立关系。  
  
 删除外键标记*TagName6*[保存]  
 删除其索引标记是外键*TagName6*。 如果省略保存，将从结构化索引中删除索引标记。 包含保存以防止从结构化的索引的索引标记的删除。  
  
 重命名列*FieldName4*收件人*FieldName5*  
 可以更改表中的字段的名称。 *FieldName4*指定已重命名字段的名称。 *FieldName5*指定字段的新名称。  
  
> [!CAUTION]  
>  由于索引表达式、 字段和表的验证规则、 命令和函数可能引用原始的字段名称重命名表字段时应格外小心。  
  
 NOVALIDATE  
 指定 Visual FoxPro 允许进行表; 的结构更改这些更改可能会违反的表中数据的完整性。 默认情况下，Visual FoxPro 阻止 ALTER TABLE 进行更改违反的表中数据的完整性。 包括 NOVALIDATE 重写此默认行为。  
  
## <a name="remarks"></a>注释  
 ALTER TABLE 可以用于修改尚未添加到数据库表的结构。 但是，如果包括默认、 外键、 主键、 引用，或修改可用的表时，SET 子句 Visual FoxPro 将生成错误。  
  
 ALTER TABLE 可能通过创建新的表头和记录追加到表标头来重建表。 例如，更改字段的类型或宽度可能会导致要重新生成的表。  
  
 重新生成表后，字段验证规则将执行的任何更改的类型或宽度的字段。 如果你更改的类型或表中的任何字段的宽度，则执行表规则。  
  
 如果你修改表中记录的字段或表验证规则，请 Visual FoxPro 测试对现有数据的新字段或表验证规则，并发出上的第一个匹配项的字段或表的验证规则或触发器冲突的警告。  
  
 如果你修改此表是在数据库中，ALTER TABLE-SQL 需要独占使用的数据库。 若要打开以供独占使用的数据库，包括打开的数据库中的独占。  
  
## <a name="see-also"></a>另请参阅  
 [创建表的 SQL 命令](../../odbc/microsoft/create-table-sql-command.md)   
 [索引命令](../../odbc/microsoft/index-command.md)

