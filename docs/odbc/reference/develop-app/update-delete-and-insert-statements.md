---
title: UPDATE、DELETE 和 INSERT 语句 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], about updating data
- DELETE [ODBC]
- UPDATE [ODBC]
- INSERT [ODBC]
- data updates [ODBC], about data updates
ms.assetid: 5004ea72-4c49-4064-9752-f7032ba7f133
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c2a2787be1bf44e1f214d396444a73b938acf7ce
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67942830"
---
# <a name="update-delete-and-insert-statements"></a>UPDATE、DELETE 和 INSERT 语句
基于 SQL 的应用程序通过执行**UPDATE**、 **DELETE**和**INSERT**语句对表进行了更改。 这些语句是最低 SQL 语法符合性级别的一部分，并且必须受所有驱动程序和数据源的支持。  
  
 这些语句的语法为：  
  
 **更新**_表-名称_  
  
 **设置**_列标识符_ **=** {*expression* &#124; **NULL**}  
  
 [**，** _列标识符_ **=** {*expression* &#124; **NULL**}] .。。  
  
 [**WHERE** _搜索条件_]  
  
 **从表中删除** _-名称_[**WHERE** _搜索条件_]  
  
 **插入**_表名称_[**（** _列标识符_[**，** _列标识符_] .。。**)**]  
  
 {*查询规范*&#124;**值（** _插入值_[**，** _插入值_] .。。**)**}  
  
 请注意，*查询规范*元素仅在核心和扩展的 sql 语法中有效，并且在核心和扩展的 sql 语法中，*表达式*和*搜索条件*元素变得更加复杂。  
  
 与其他 SQL 语句一样， **UPDATE**、 **DELETE**和**INSERT**语句在使用参数时效率更高。 例如，可以为以下语句做好准备并重复执行以在 Orders 表中插入多行：  
  
```  
INSERT INTO Orders (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 通过传递参数值的数组，可以提高这一效率。 有关参数值的语句参数和数组的详细信息，请参阅[语句参数](../../../odbc/reference/develop-app/statement-parameters.md)。
