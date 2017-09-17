---
title: "索引命令 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- index command [ODBC]
ms.assetid: 694e8cf5-2f69-4001-9c1e-b735a4da3aff
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: cdec619d99c610c75b9b27de710cd4e5913602f6
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="index-command"></a>索引命令
创建要显示和访问表记录按逻辑顺序排列的索引文件。  
  
## <a name="syntax"></a>语法  
  
```  
  
INDEX ON eExpression TO IDXFileName | TAG TagName [OF CDXFileName]  
   [FOR lExpression]  
   [COMPACT]  
   [ASCENDING | DESCENDING]  
   [UNIQUE | CANDIDATE]  
   [ADDITIVE]  
```  
  
## <a name="arguments"></a>参数  
 *eExpression*  
 指定一个索引表达式，可以包括或从当前表的多个字段的名称。 索引键基于索引表达式是在表中每个记录的索引文件中创建的。 Visual FoxPro 使用这些密钥来显示和访问表中的记录。  
  
> [!NOTE]  
>  尽管不建议这样做， *eExpression*也可以是内存变量，数组元素，或字段或字段表达式从另一个工作区中的表。 在索引文件表达式; 中不能单独使用备注字段它们必须与其他字符表达式组合。 如果你访问包含的变量或字段不再存在或找不到索引，则 Visual FoxPro 生成一条错误消息。  
  
 如果你尝试使用不同长度的密钥生成索引，则将使用空格填充密钥。 长度可变的索引键中 Visual FoxPro 不受支持。  
  
 很可能使用长度为零创建索引键。 例如，当索引表达式为空的备注字段的子字符串时，会创建零长度索引键。 零长度索引键生成一条错误消息。 当 Visual FoxPro 创建索引时，它会计算表中的第一个记录中的字段。 如果字段为空，可能有必要在第一条记录以防止 0 长度索引键中的字段中输入一些临时数据。  
  
 到*IDXFileName*  
 创建一个.idx 索引文件。 索引的文件都有默认扩展.idx。  
  
 标记*TagName*[OF *CDXFileName*]  
 创建复合索引文件。 复合索引文件是单个索引文件，其中包含任意数量的单独的标记 （索引条目）。 由其唯一标记名称标识每个标记。 标记名称必须以字母或下划线开头，并且可以包含的最多 10 个字母、 数字或下划线的任意组合。 复合索引文件中的标记数仅受可用内存和磁盘空间。  
  
 多个条目复合索引文件都始终处于 compact。 无需创建复合索引文件时包括压缩。 复合索引文件的名称将被赋予.cdx 扩展。  
  
 可以创建两种类型的复合索引文件： 结构化和非结构性。  
  
 **结构化的复合索引文件**可以使用标记创建结构化的复合索引文件*TagName*通过排除可选的*CDXFileName*子句。 结构化的复合索引文件始终具有与表相同的基名称，并打开表时自动打开。  
  
 **非结构性复合索引文件**可以通过添加的创建非结构性复合索引文件*CDXFileName*标记之后*TagName*。 像结构复合索引的文件，非结构性复合索引文件必须显式打开带有索引子句中使用。  
  
 如果已创建并打开复合索引文件，并发出具有标记的索引*TagName*将标记添加到复合索引文件。  
  
 有关*lExpression*  
 凭此指定的条件满足筛选器表达式的记录*lExpression*可用于显示和访问; 在筛选器表达式匹配的那些记录的索引文件中创建索引键。  
  
 Visual FoxPro Rushmore 技术优化索引...有关*lExpression*命令如果*lExpression*是一个可优化的表达式。 为了获得最佳性能，使用 FOR 子句中的可优化表达式。  
  
 压缩  
 创建一个 compact.idx 文件。  
  
 升序  
 指定一个按升序.cdx 文件。 默认情况下，会以升序创建.cdx 标记。 （你可以包括升序作为索引文件的顺序的提醒。）可以按包括降序按相反的顺序索引表。  
  
 降序  
 指定.cdx 文件的降序顺序。 在创建.idx 索引文件时，不能包括降序。  
  
 UNIQUE  
 指定仅在遇到具有特定索引键值的第一个记录纳入.idx 文件或一个.cdx 标记。 唯一可用来阻止对重复记录的显示或访问。 从索引文件中排除添加具有重复的索引键的所有记录。 使用索引的唯一选项等同于发证索引或重新编制索引之前执行 SET UNIQUE ON。  
  
 当唯一索引或索引标记为活动状态，以更改其索引键的方式更改重复记录，将更新索引或索引标记。 但是，不能访问原始索引键的下一步重复记录或将其显示，直到重新索引使用重新编制索引的文件。  
  
 候选  
 创建一个候选结构索引标记。 仅当创建结构化索引标记; 时，才可以包含候选关键字否则，Visual FoxPro 生成一条错误消息。  
  
 候选索引标记可阻止重复值的字段或字段索引表达式中指定的组合中*eExpression*。 术语*候选*索引; 的类型是指由于候选索引阻止重复的值，因此它们符合的条件的"候选"主索引。  
  
 Visual FoxPro 生成错误，如果创建候选索引标记的字段或字段的已包含重复值的组合。  
  
 累加性  
 保持打开的任何先前已打开的索引文件。 如果省略累加性子句使用索引创建的索引文件或表的文件时，将关闭 （除外的结构化的复合索引） 的任何先前已打开的索引文件。  
  
## <a name="remarks"></a>注释  
 表包含索引文件中的记录显示和访问索引表达式所指定的顺序。 物理表中记录的顺序未被索引文件更改。  
  
## <a name="index-types"></a>索引类型  
 Visual FoxPro，可以创建两种类型的索引文件：  
  
-   复合.cdx 索引文件，其中包含调用标记的多个索引项  
  
-   包含一个索引条目.idx 索引文件  
  
 你还可以创建一个结构的复合索引文件，其中将自动打开，其中的表。  
  
> [!NOTE]  
>  由于打开表时自动打开结构复合索引文件，它们是首选的索引类型。  
  
 包括 COMPACT 创建 compact.idx 索引文件。 复合索引文件都始终处于 compact。  
  
## <a name="index-order-and-updating"></a>索引订单和更新  
 只有一个索引文件 （主索引文件） 或标记 （master 标记） 控制在其中显示或访问表的顺序。 某些命令 （例如查找） 使用的主索引文件或标记以搜索记录。 但是，所有打开.idx 和.cdx 索引的文件将更新到表做出更改。  
  
## <a name="user-defined-functions"></a>用户定义函数  
 虽然索引表达式可以包含用户定义函数，但不应在索引表达式中使用用户定义函数。 索引表达式中的用户定义函数增加创建或更新索引所需的时间。 此外，用户定义函数用于索引表达式时，不可能发生索引更新。  
  
 索引表达式中使用用户定义函数，如果 Visual FoxPro 必须能够找到用户定义函数。 当 Visual FoxPro 创建索引时，索引表达式将保存在索引文件，但仅对用户定义函数的引用并包括索引表达式中。  
  
## <a name="see-also"></a>另请参阅  
 [更改表的 SQL 命令](../../odbc/microsoft/alter-table-sql-command.md)   
 [删除标记命令](../../odbc/microsoft/delete-tag-command.md)   
 [SET COLLATE 命令](../../odbc/microsoft/set-collate-command.md)   
 [SET 唯一命令](../../odbc/microsoft/set-unique-command.md)
