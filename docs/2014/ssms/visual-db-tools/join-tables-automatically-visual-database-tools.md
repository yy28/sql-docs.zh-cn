---
title: 自动联接表 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- automatic joins
- joins [SQL Server], creating
- joins [SQL Server], automatic
ms.assetid: f152af82-bcb6-49ca-af19-48cdb7fc9ac6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bab311878966087ef9b6c3f05bb3023d02fdeb20
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62711064"
---
# <a name="join-tables-automatically-visual-database-tools"></a>自动联接表 (Visual Database Tools)
  将两个或多个表添加到查询中时， [查询和视图设计器](visual-database-tools.md) 会尝试确定它们是否相关。 如果相关，查询和视图设计器将自动在表示表或表结构对象的矩形之间添加联接线。  
  
 如果满足以下条件，查询和视图设计器就会将表识别为联接的表：  
  
-   数据库包含指定这些表相关的信息。  
  
-   如果两个表各有一列具有相同的名称和数据类型。 该列必须至少在一个表中是主键。 例如，假设添加 `employee` 和 `jobs` 表，如果 `job_id` 列是 `jobs` 表的主键，并且两个表中都有一个名为 `job_id` 的列，且具有相同的数据类型，那么查询和视图设计器将自动联接这两个表。  
  
    > [!NOTE]  
    >  查询和视图设计器根据具有相同名称和数据类型的列只能创建一个联接。 如果有多种联接可能，查询和视图设计器在根据所找到的第一组匹配列创建一个联接后即会停止。  
  
-   查询和视图设计器可以检测到搜索条件（WHERE 子句）实际上是否为联接条件。 例如，假设您添加表 `employee` 和 `jobs`，再创建一个搜索条件，搜索这两个表的 `job_id` 列中的相同值。 当执行搜索时，查询和视图设计器可检测到该搜索条件会导致联接，就会根据该搜索条件创建联接条件。  
  
 如果查询和视图设计器创建了一个不适合于您的查询的联接，您可以修改或移除该联接。 有关详细信息，请参阅[修改联接运算符 (Visual Database Tools)](modify-join-operators-visual-database-tools.md) 和[删除联接 (Visual Database Tools)](remove-joins-visual-database-tools.md)。  
  
 如果查询和视图设计器在查询中没有自动联接表，您可以自己创建联接。 有关详细信息，请参阅[手动联接表 (Visual Database Tools)](join-tables-manually-visual-database-tools.md)。  
  
## <a name="see-also"></a>另请参阅  
 [查询和视图设计器如何表示 &#40;Visual Database Tools 的联接&#41;](how-the-query-and-view-designer-represents-joins-visual-database-tools.md)   
 [&#40;Visual Database Tools 的设计查询和视图操作指南主题&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)   
 [使用联接进行查询 (Visual Database Tools)](query-with-joins-visual-database-tools.md)  
  
  
