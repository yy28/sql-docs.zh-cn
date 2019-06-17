---
title: 使用未命名参数创建查询 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- unnamed parameters
- parameters [SQL Server], unnamed
ms.assetid: 5f4b664b-3d3d-4d07-a0e7-791d78743504
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 2738825a94b2acd067f24b06178eff1817bf0519
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65095668"
---
# <a name="create-queries-with-unnamed-parameters-visual-database-tools"></a>使用未命名参数创建查询 (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
可通过将问号 (?) 指定为文字值的占位符来使用未命名参数创建查询。 查询和视图设计器将为未命名参数指定临时名称。 可根据需要在查询中指定任意数目的未命名参数。  
  
在查询和视图设计器中运行查询时，将显示“查询参数”对话框，同时显示临时名称。  
  
### <a name="to-specify-an-unnamed-parameter"></a>指定未命名参数  
  
1.  将要搜索的列或表达式添加到 [“条件”窗格](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)中。 如果不希望搜索列或表达式出现在查询输出中，则将其从输出列中移除。  
  
2.  找到包含要搜索的数据列或表达式的行，然后在“筛选器”  网格列中输入一个问号 (?)。  
  
    默认情况下，查询和视图设计器将添加“=”运算符。 不过，您可以对该单元格进行编辑，以替换“>”、“<”或任何其他 SQL 比较运算符。  
  
## <a name="see-also"></a>另请参阅  
[使用参数进行查询 (Visual Database Tools)](../../ssms/visual-db-tools/query-with-parameters-visual-database-tools.md)  
  
