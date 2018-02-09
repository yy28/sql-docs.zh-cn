---
title: "错误处理 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- reporting errors [ADO]
- errors [ADO]
- ADO, error handling
ms.assetid: 4909e413-f3b0-4183-8ad3-67b1434df742
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: eeb8b4abe5d199e3887b526c77163dcb8f1272fb
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="error-handling"></a>错误处理
ADO 使用多种不同方法来通知出现的错误的应用程序。 本部分讨论使用 ADO 和如何通知你的应用程序时可能发生的错误的类型。 则可以确定通过进行有关如何处理这些错误的建议。  
  
## <a name="how-does-ado-report-errors"></a>ADO 如何报告错误？  
 ADO 会通知你有关以下几种方式的错误：  
  
-   ADO 错误会生成运行时错误。 就像任何其他运行时错误，例如，使用相同的方式处理 ADO 错误**On Error**在 Visual Basic 中的语句。  
  
-   程序可以接收来自 OLE DB 错误。 OLE DB 错误生成了的运行时错误。  
  
-   如果错误是特定于你的数据提供程序，一个或多个**错误**对象都将置于**错误**集合**连接**用于访问数据的对象存储时出错。  
  
-   如果引发事件的过程也产生了错误，错误信息放置在**错误**对象，并作为参数传递的事件。 请参阅[处理 ADO 事件](../../../ado/guide/data/handling-ado-events.md)有关事件的详细信息。  
  
-   处理过程中发生的问题批处理更新或其他大容量操作涉及**记录集**可以由**状态**属性**记录集**。 例如，通过指定架构约束冲突或权限不足，无法**RecordStatusEnum**值。  
  
-   发生涉及特定的问题**字段**由还指示当前记录中**状态**每个属性**字段**中**字段**集合**记录**或**记录集**。 例如，通过指定数据类型不兼容或无法完成的更新**FieldStatusEnum**值。  
  
 本部分包含以下主题。  
  
-   [ADO 错误](../../../ado/guide/data/ado-errors.md)  
  
-   [提供程序错误](../../../ado/guide/data/provider-errors.md)  
  
-   [字段相关错误信息](../../../ado/guide/data/field-related-error-information.md)  
  
-   [记录集相关错误信息](../../../ado/guide/data/recordset-related-error-information.md)  
  
-   [处理其他语言中的处理错误](../../../ado/guide/data/handling-errors-in-other-languages.md)  
  
-   [预测错误](../../../ado/guide/data/anticipating-errors.md)
