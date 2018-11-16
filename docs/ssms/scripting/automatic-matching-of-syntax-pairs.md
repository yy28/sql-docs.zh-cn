---
title: 语法对的自动匹配 | Microsoft Docs
ms.date: 03/01/2017
ms.prod: sql
ms.technology: scripting
ms.topic: conceptual
helpviewer_keywords:
- IntelliSense [SQL Server], delimiter highlighting
- IntelliSense [SQL Server], syntax pair matching
ms.assetid: bfc54cda-bfd6-4545-a5b9-f9db2ae13769
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 28f2a51773c4232e4507cb06cba0d6b96a6cae93
ms.sourcegitcommit: 0638b228980998de9056b177c83ed14494b9ad74
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/14/2018
ms.locfileid: "51642957"
---
# <a name="automatic-matching-of-syntax-pairs"></a>语法对的自动匹配
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  使用自动匹配语法对功能，可获得有关必须以成对方式进行编码的语法元素是否正确配对的即时反馈。 这种匹配在 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查询编辑器中被称为分隔符匹配，在 Analysis Services XMLA 查询编辑器中被称为大括号匹配，而在 MDX 和 DMX 编辑器中则被称为圆括号匹配。  
  
## <a name="database-engine-query-editor-delimiter-matching"></a>数据库引擎查询编辑器的分隔符匹配  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 查询编辑器与标识代码块边界的分隔符相匹配。 有两种匹配方式：  
  
-   键入成对分隔符中的第二个分隔符后，该编辑器将突出显示此对分隔符中的两个分隔符。  
  
-   只要光标位于一对分隔符中的其中一个分隔符中，就可使用 Ctrl+] 键盘快捷键跳转到与之相匹配的分隔符。  
  
### <a name="delimiter-pairs"></a>成对分隔符  
 自动分隔符匹配可识别以下几组分隔符：  
  
|前导分隔符|结尾分隔符|  
|--------------------|-----------------------|  
|**(**|**)**|  
|**BEGIN**|**END**|  
|**BEGIN TRY**|**END TRY**|  
|**BEGIN CATCH**|**END CATCH**|  
  
 自动分隔符匹配不识别中括号标识符 ([ObjectName]) 或引号标识符 ("ObjectName") 之类的分隔符。 由于颜色编码已形象地指示出字符串是否已进行分隔，因此成对分隔符匹配功能与字符串文字 ('string') 的单引号分隔符不匹配。  
  
### <a name="delimiter-highlighting"></a>分隔符的突出显示  
 匹配突出显示一对分隔符的前导和结尾元素， 从而便于您直观地识别代码块并检查不匹配的分隔符对。  
  
 键入结束成对分隔符的最后一个字母后，分隔符将突出显示出来。 例如，对于一对 BEGIN END 分隔符，首先键入 BEGIN，然后键入 END，在键入 END 的最后一个字母 D 时，将打开突出显示。 但不必通过先键入前导分隔符，再键入结尾分隔符的方式来启动突出显示。 如果先键入 END，然后向上回滚脚本并键入 BEGIN，则在键入 BEGIN 的最后一个字母 N 时，将启用突出显示。 但最后键入的字母不一定是分隔符的结尾字母。 例如，有可能将 BEGIN 错拼成 BEIN，则在插入最后一个字母 G 时，将突出显示该 BEGIN END 对。  
  
 移动光标之前，该对分隔符将保持突出显示状态。 移动光标后，将关闭突出显示，即使新光标位置仍在同一分隔符中时也是如此。 删除并重新键入该对分隔符任一成员中的任一字母即可重新启用突出显示。  
  
## <a name="analysis-services-xmla-query-editor-brace-matching"></a>Analysis Services XMLA 查询编辑器的大括号匹配  
 XMLA 查询编辑器的大括号匹配通过突出显示左右大括号来显示是否存在闭合的元素。 还可使用 Ctrl+] 键盘快捷键从一个大括号跳转到与其匹配的大括号。  
  
 XMLA 查询编辑器对以下项进行大括号匹配：  
  
-   匹配的开始和结束标记。  
  
-   任何成对的“\<”和“>”尖括号。  
  
-   注释的开头和结尾。  
  
-   处理指令的开头和结尾。  
  
-   CDATA 块的开头和结尾。  
  
-   DTD 声明的开头和结尾。  
  
-   属性的左右引号。  
  
## <a name="mdx-and-dmx-editor-parenthesis-matching"></a>MDX 和 DMX 编辑器的圆括号匹配  
 多维表达式 (MDX) 和数据挖掘表达式 (DMX) 编辑器自动匹配函数中的成对圆括号。
