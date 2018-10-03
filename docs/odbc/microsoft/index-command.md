---
title: INDEX 命令 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e0af3a454963474df483c56e5afddaede77b29dd
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47721065"
---
# <a name="index-command"></a>INDEX 命令
创建一个索引文件，以显示和访问表记录按逻辑顺序。  
  
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
 指定一个索引表达式，可以包含的字段或字段从当前表的名称。 索引键基于索引表达式中的索引文件的表中每个记录创建。 Visual FoxPro 使用这些密钥来显示和访问表中的记录。  
  
> [!NOTE]  
>  尽管不建议这样做*eExpression*也可以是内存变量、 数组元素，或字段或从另一个工作区中的表的字段表达式。 备注字段不能单独使用索引文件表达式; 中它们必须与其他字符表达式组合。 如果访问包含的变量或字段不再存在或找不到的索引时，Visual FoxPro 生成一条错误消息。  
  
 如果尝试在长度发生变化的密钥生成索引，将用空格填充该键。 长度可变的索引键中 Visual FoxPro 不受支持。  
  
 就可以创建具有长度为零的索引键。 例如，将零长度索引创建密钥，当索引表达式为空的备注字段的子字符串。 零长度索引键生成一条错误消息。 当 Visual FoxPro 创建索引时，它会评估中的表中的第一个记录的字段。 如果字段为空，可能需要在第一条记录以防止长度 0 的索引键中的字段中输入一些临时数据。  
  
 到*IDXFileName*  
 创建一个.idx 索引文件。 索引的文件都有默认扩展.idx。  
  
 标记*TagName*[OF *CDXFileName*]  
 创建复合索引文件。 复合索引文件是包含任意数量的单独的标记 （索引条目） 的单个索引文件。 每个标记都由其唯一的标记名称标识。 标记名称必须以字母或下划线开头，并且可以包含最多 10 个字母、 数字或下划线的任意组合。 复合索引文件中的标记数仅受可用内存和磁盘空间。  
  
 多个条目复合索引文件始终是 compact。 它不需要包括 COMPACT 创建复合索引文件时。 复合索引文件的名称将被赋予.cdx 扩展。  
  
 可以创建复合索引文件的两种类型： 结构化和非结构性。  
  
 **结构化的复合索引文件**可以使用标记创建结构复合索引文件*TagName*通过排除可选 OF *CDXFileName*子句。 结构复合索引文件始终具有与表相同的基名称，并将自动打开时打开的表。  
  
 **非结构性复合索引文件**可以创建非结构性复合索引文件通过包括 OF *CDXFileName*标记之后*TagName*。 与结构化的复合索引文件不同非结构性复合索引文件必须使用在 INDEX 子句中使用显式打开。  
  
 如果已创建并打开复合索引文件，并发出具有标记的索引*TagName*将标记添加到复合索引文件。  
  
 有关*lExpression*  
 指定的条件，满足筛选表达式条件的记录*lExpression*可用于显示和访问权限; 索引密钥创建的索引文件的筛选器表达式匹配的那些记录。  
  
 Visual FoxPro 雕像技术来优化索引...有关*lExpression*命令的命令*lExpression*是一个可优化的表达式。 为了获得最佳性能的 FOR 子句中使用的可优化的表达式。  
  
 压缩  
 创建一个 compact.idx 文件。  
  
 升序  
 指定升序顺序.cdx 文件。 默认情况下，.cdx 标记创建按升序排序。 （您可以包括升序索引文件的顺序的提醒。）可以通过包括降序按相反的顺序索引表。  
  
 降序  
 指定降序.cdx 文件。 创建.idx 索引文件时，不能包含降序。  
  
 UNIQUE  
 指定包含.idx 文件或.cdx 标记中，必须仅具有特定索引键值遇到第一条记录。 唯一可用于阻止对重复记录的内容的显示或访问。 添加具有重复的索引键的所有记录都不从索引文件。 使用索引的唯一选项是相同的颁发重新编制索引之前执行 SET UNIQUE ON。  
  
 唯一索引或索引标记为活动状态，以更改其索引键的方式更改重复记录时将更新的索引或索引标记。 但是下, 一步的重复记录与原始索引键不能访问或显示，直到重新建立索引使用重新编制索引的文件。  
  
 候选项  
 创建一个候选结构化索引标记。 仅当创建一个结构化索引标记; 时，才可以包含候选关键字否则，Visual FoxPro 生成一条错误消息。  
  
 候选索引标记可防止重复值中的字段或索引表达式中指定的字段的组合*eExpression*。 术语*候选*所引用的索引; 的类型候选索引避免重复的值，因为它们符合的条件"候选人"作为主索引。  
  
 Visual FoxPro 生成错误，如果您创建的字段或字段的已包含重复值的组合的候选索引标记。  
  
 累加性  
 保留打开的任何以前打开的索引文件。 如果省略累加性子句时使用索引创建索引或表的文件，，关闭 （除了结构化的复合索引） 的任何以前打开的索引文件。  
  
## <a name="remarks"></a>备注  
 表具有一个索引文件中的记录显示，和由索引表达式指定的顺序访问。 表中记录的物理顺序不会更改由索引文件。  
  
## <a name="index-types"></a>索引类型  
 Visual FoxPro 允许您创建两种类型的索引文件：  
  
-   复合包含多个索引条目调用标记的.cdx 索引文件  
  
-   包含一个索引条目.idx 索引文件  
  
 此外可以创建一个结构复合索引文件，其中使用表将自动打开。  
  
> [!NOTE]  
>  在打开的表时自动打开的结构化的复合索引文件，因为它们是首选的索引类型。  
  
 包括 COMPACT 创建 compact.idx 索引文件。 复合索引文件始终是 compact。  
  
## <a name="index-order-and-updating"></a>索引顺序和更新  
 只有一个索引文件 （主索引文件） 或标记 （主标记） 控制在其中显示或访问表的顺序。 某些命令 （例如查找） 使用的主索引文件或标记以搜索记录。 但是，所有打开的.idx 并对表做出更改后更新.cdx 索引文件。  
  
## <a name="user-defined-functions"></a>用户定义函数  
 尽管索引表达式可以包含用户定义函数，但不应在索引表达式中使用用户定义的函数。 索引表达式中的用户定义函数增加创建或更新索引花费的时间。 此外，索引更新可能不会出现的用户定义函数用于索引表达式时。  
  
 如果在索引表达式中使用的用户定义函数，Visual FoxPro 必须能够找到用户定义函数。 当 Visual FoxPro 创建索引时，索引表达式保存在索引文件，但仅对用户定义函数的引用包含在索引表达式。  
  
## <a name="see-also"></a>请参阅  
 [ALTER TABLE-SQL 命令](../../odbc/microsoft/alter-table-sql-command.md)   
 [DELETE TAG 命令](../../odbc/microsoft/delete-tag-command.md)   
 [SET COLLATE 命令](../../odbc/microsoft/set-collate-command.md)   
 [SET UNIQUE 命令](../../odbc/microsoft/set-unique-command.md)
