---
title: “全文索引列”对话框 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.fulltextcolumn
ms.assetid: a6f41c5c-d950-4d64-9e42-d062925917b6
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 972f556315a9ff8c1042973aed118705bb815507
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2018
ms.locfileid: "43815573"
---
# <a name="full-text-index-columns-dialog-box-visual-database-tools"></a>“全文本索引列”对话框 (Visual Database Tools)
  此对话框列出了参与表设计器中所打开表的全文本索引的列。 若要访问此对话框，请在表设计器中右键单击相应的表，选择“全文检索”，然后在“全文检索”对话框中，单击具有要查看或编辑的列的索引，单击右侧网格中的“列”字段，再单击省略号 (**…**)。  
  
## <a name="options"></a>选项  
 **列**  
 显示参与全文本索引的列的名称。 若要添加列，请单击第一个空单元格，再从下拉列表中选择列。 只能基于文本的数据类型或 image 数据类型的列才可访问。  
  
 **数据类型**  
 显示每列的数据类型。 此属性是只读属性。 若要更改数据类型，请在表设计器中打开表，单击相应列，然后在“列属性”选项卡中编辑数据类型。  
  
 **按列分类**  
 仅适用于数据类型为 `image` 的列。 提供一个下拉列表，可以从中选择其他列中哪一列代表此列的数据类型。 如果此列的数据类型不是 `image`，则该值将为“无”。  
  
 数据类型为 `image` 的列可以包含 Microsoft Office 文件（.doc、.xls 和 .ppt 文件）、文本文件（.txt 文件）和 HTML 文件（.htm 文件），将该列的数据类型设置为 image 将允许进行全文搜索以搜索文件的内容。  
  
 **语言**  
 列出可用语言。 从下拉列表中选择适合您的列数据的语言。 例如，如果您使用的是英语版本的操作系统，但希望对包含德文的列进行索引，请从下拉列表中选择“德语”以提高索引的性能。  
  
 **统计语义**  
 选择是否为所选列启用语义索引。 有关详细信息，请参阅[语义搜索 (SQL Server)](../../relational-databases/search/semantic-search-sql-server.md)。  
  
 如果您在选择 **“统计语义”** 前选择某一 **“语言”**，并且所选语言没有关联的语义语言模型，则 **“统计语义”** 复选框将被禁用。 如果你在选择“语言”前选择“统计语义”，则下拉组合框中提供的语言将限制为存在语义语言模型支持的那些语言。  
  
## <a name="see-also"></a>请参阅  
 [“全文检索”对话框 (Visual Database Tools)](visual-database-tools.md)  
  
  
