---
title: INDEX 命令 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- index command [ODBC]
ms.assetid: 694e8cf5-2f69-4001-9c1e-b735a4da3aff
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bcb30a49cb9f11ddd4c61621116aa4bd8ddcf186
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300027"
---
# <a name="index-command"></a>INDEX 命令
创建索引文件以按逻辑顺序显示和访问表记录。  
  
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
 *e表达式*  
 指定一个索引表达式，该表达式可以包含当前表中的字段或字段的名称。 在表中每个记录的索引文件中创建基于索引表达式的索引键。 Visual FoxPro 使用这些键来显示和访问表中的记录。  
  
> [!NOTE]  
>  尽管不推荐*eExpression，* 但也可以是内存变量、数组元素或来自另一个工作区表中的字段或字段表达式。 备忘录字段不能单独用于索引文件表达式;因此，在索引文件表达式中，不能单独使用备忘录字段。它们必须与其他字符表达式组合。 如果您访问包含不再存在或找不到的变量或字段的索引，Visual FoxPro 将生成错误消息。  
  
 如果尝试使用长度不同的键生成索引，则该键将填充空格。 Visual FoxPro 不支持可变长度索引键。  
  
 可以创建长度为零的索引键。 例如，当索引表达式是空备忘录字段的子字符串时，将创建零长度索引键。 零长度索引键生成错误消息。 当 Visual FoxPro 创建索引时，它会评估表中第一条记录中的字段。 如果字段为空，则可能需要在第一个记录中的字段中输入一些临时数据，以防止 0 长索引键。  
  
 到*IDX 文件名*  
 创建 .idx 索引文件。 索引文件为默认扩展名 .idx 指定。  
  
 *标签标签名称* *[CDX 文件名 ]*  
 创建复合索引文件。 复合索引文件是一个索引文件，由任意数量的单独的标记（索引条目）组成。 每个标记都由其唯一的标记名称标识。 标记名称必须以字母或下划线开头，并且可以由最多 10 个字母、数字或下划线组成的任意组合组成。 复合索引文件中的标记数仅受可用内存和磁盘空间的限制。  
  
 多条目复合索引文件始终紧凑。 创建复合索引文件时，无需包括 COMPACT。 复合索引文件的名称为 .cdx 扩展名。  
  
 可以创建两种类型的复合索引文件：结构和非结构。  
  
 **结构复合索引文件**您可以通过排除可选的 OF *CDXFileName*子句来创建带有*TAG Name*的结构复合索引文件。 结构复合索引文件始终与表具有相同的基本名称，并在打开表时自动打开。  
  
 **非结构复合索引文件**您可以通过在 TAG *TagName*后包括 OF *CDXFileName*来创建非结构复合索引文件。 与结构复合索引文件不同，非结构复合索引文件必须使用 USE 中的 INDEX 子句显式打开。  
  
 如果已创建并打开复合索引文件，则使用*TAG TagName*发出 INDEX 会向复合索引文件添加标记。  
  
 对于*l 表达式*  
 指定一个条件，即只有满足筛选器表达式*lExpression*的记录才能显示和访问;索引键在索引文件中只为与筛选器表达式匹配的记录创建。  
  
 可视化福克斯Pro拉什莫尔技术优化INDEX...对于*lExpression 命令*（如果*lExpression*是可优化的表达式）。 为获得最佳性能，请使用 FOR 子句中的可优化表达式。  
  
 紧凑  
 创建紧凑的 .idx 文件。  
  
 上升  
 指定 .cdx 文件的升序。 默认情况下，.cdx 标记按升序创建。 （您可以包括 ASCENDING 作为索引文件订单的提醒。可以通过包括降序，以相反的顺序对表进行索引。  
  
 降  
 指定 .cdx 文件的降序。 创建 .idx 索引文件时，不能包括降序。  
  
 UNIQUE  
 指定仅在 .idx 文件或 .cdx 标记中包含与特定索引键值遇到的第一个记录。 UNIQUE 可用于防止显示或访问重复记录。 使用重复索引键添加的所有记录都从索引文件中排除。 使用 INDEX 的"唯一"选项与在发出 INDEX 或 REINDEX 之前执行 SET UNIQUE ON 相同。  
  
 当 UNIQUE 索引或索引标记处于活动状态，并且重复记录以更改其索引键的方式更改时，将更新索引或索引标记。 但是，在使用 REINDEX 重新索引文件之前，无法访问或显示具有原始索引键的下一个重复记录。  
  
 候选人  
 创建候选结构索引标记。 仅当创建结构索引标记时，才能包含候选关键字;否则，Visual FoxPro 会生成错误消息。  
  
 候选索引标记可防止字段中重复的值或索引*表达式 eExpression*中指定的字段的组合。 术语 *"候选"* 是指索引的类型;由于候选索引可防止重复值，因此它们有资格作为"候选"作为主索引。  
  
 如果为字段或已包含重复值的字段组合创建候选索引标记，则 Visual FoxPro 将生成错误。  
  
 添加剂  
 保持打开任何以前打开的索引文件。 如果在为索引文件或具有 INDEX 的表创建索引文件时省略了 ADDITIVE 子句，则关闭以前打开的任何索引文件（结构复合索引除外）。  
  
## <a name="remarks"></a>备注  
 具有索引文件的表中的记录按索引表达式指定的顺序显示和访问。 索引文件不会更改表中记录的物理顺序。  
  
## <a name="index-types"></a>索引类型  
 Visual FoxPro 允许您创建两种类型的索引文件：  
  
-   包含多个称为标记的索引条目的复合 .cdx 索引文件  
  
-   .idx 索引文件包含一个索引条目  
  
 您还可以创建结构复合索引文件，该文件会自动打开表。  
  
> [!NOTE]  
>  由于结构复合索引文件在打开表时会自动打开，因此它们是首选索引类型。  
  
 包括 COMPACT 以创建紧凑的 .idx 索引文件。 复合索引文件总是紧凑的。  
  
## <a name="index-order-and-updating"></a>索引顺序和更新  
 只有一个索引文件（主索引文件）或标记（主标记）控制表的显示或访问顺序。 某些命令 （例如，SEEK） 使用主索引文件或标记来搜索记录。 但是，所有打开的 .idx 和 .cdx 索引文件都随着对表的更改而更新。  
  
## <a name="user-defined-functions"></a>用户定义函数  
 尽管索引表达式可以包含用户定义的函数，但不应在索引表达式中使用用户定义的函数。 索引表达式中的用户定义的函数会增加创建或更新索引所需的时间。 此外，当用户定义的函数用于索引表达式时，可能不会发生索引更新。  
  
 如果在索引表达式中使用用户定义的函数，Visual FoxPro 必须能够找到用户定义的函数。 当 Visual FoxPro 创建索引时，索引表达式将保存在索引文件中，但索引表达式中仅包含对用户定义的函数的引用。  
  
## <a name="see-also"></a>另请参阅  
 [更改表 - SQL 命令](../../odbc/microsoft/alter-table-sql-command.md)   
 [删除 TAG 命令](../../odbc/microsoft/delete-tag-command.md)   
 [设置隔离命令](../../odbc/microsoft/set-collate-command.md)   
 [SET UNIQUE 命令](../../odbc/microsoft/set-unique-command.md)
