---
title: 验证查询 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdtsql.chm:100644
helpviewer_keywords:
- verifying queries
- queries [SQL Server], verifying
- checking queries
ms.assetid: 1382c0c0-46dc-45f9-ab38-9bba1d347eea
author: stevestein
ms.author: sstein
ms.openlocfilehash: 7bf24de9bdc0e8b7b7ceb33bb881812b180ce112
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85064252"
---
# <a name="verify-queries-visual-database-tools"></a>验证查询 (Visual Database Tools)
  为了避免问题，可以对所生成的查询进行检查以确保其语法正确。 在 [SQL 窗格](visual-database-tools.md)中输入语句时，此选项尤其有用。  
  
 在验证查询时应谨记以下几点：  
  
-   即使无法在“关系图”  窗格和“条件”  窗格中表示某个语句，该语句也可能是有效的，因此可以通过验证。  
  
-   SQL 验证可检测某些 SQL 错误，但不能检测所有 SQL 错误。 如果查询包含在 SQL 验证过程中未检测到的错误，则在运行该查询时，数据库将检测到该错误。  
  
-   无法对包含参数的查询进行验证。  
  
### <a name="to-verify-an-sql-statement"></a>验证 SQL 语句  
  
-   右键单击“SQL 窗格”  ，然后从快捷菜单中选择“验证 SQL 语法”  。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;Visual Database Tools 运行查询&#41;](run-queries-visual-database-tools.md)   
 [执行基本的查询操作 (Visual Database Tools)](perform-basic-operations-with-queries-visual-database-tools.md)  
  
  
