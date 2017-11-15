---
title: "“排序规则”对话框 (Visual Database Tools) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vdt.dlgbox.definecolumncollation
- vdtsql.chm:65561
ms.assetid: e4020f79-7abf-4839-b9b2-984ef7049817
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 16504f76025571fa7627027ba37267aac6e41a41
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="collation-dialog-box-visual-database-tools"></a>“排序规则”对话框 (Visual Database Tools)
使用此对话框可为列指定排序规则顺序。 列的排序规则顺序可用在将列值与其他列的值或常量值进行比较的各项操作中。 它还会影响一些字符串函数（如 SUBSTRING 和 CHARINDEX）的行为。 有关列排序规则设置的效果的完整列表，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 文档。  
  
在以下情况下将显示此对话框：  
  
-   在“列属性”选项卡的“排序规则”字段中输入无效的排序规则名称。  
  
-   在“列属性”选项卡的“排序规则”字段中单击，再单击该字段右侧的省略号按钮 **(…)**。  
  
## <a name="options"></a>选项  
**SQL 排序规则**  
在下拉列表中由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 定义的排序规则顺序之间进行选择。  
  
**Windows 排序规则**  
在下拉列表中由 Windows 定义的排序规则顺序之间进行选择。  
  
**二进制排序**  
使用字符值的二进制代码进行比较。 如果选择此选项，某些字母比较选项将不可用。 例如，不区分大小写的比较选项将不可用，因为大写字母和小写字母具有不同的二进制编码。 只有在选择了“Windows 排序规则”后才适用。  
  
**字典排序**  
使用字母比较选项。 只有在选择了“Windows 排序规则”后才适用。 字母比较选项包括：  
  
-   **区分大小写** 如果希望在比较中将大写字母和小写字母视为不相同，请选择此选项。  
  
-   **区分重音** 如果希望在比较中将重音字母和非重音字母视为不相同，请选择此选项。 如果选择此选项，在比较中还会将重音位于不同字母的情况视为不相同。  
  
-   **区分假名** 如果希望在比较中将片假名和平假名日语音节视为不相同，请选择此选项。  
  
-   **区分全半角** 如果希望在比较中将半角字符和全角字符视为不相同，请选择此选项。  
  
**“恢复默认值”按钮**  
向列应用数据库的默认排序规则顺序。  
  
## <a name="see-also"></a>另请参阅  
[在聚合查询中使用列 (Visual Database Tools)](../../ssms/visual-db-tools/work-with-columns-in-aggregate-queries-visual-database-tools.md)  
  
