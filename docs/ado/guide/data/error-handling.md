---
title: 错误处理 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- reporting errors [ADO]
- errors [ADO]
- ADO, error handling
ms.assetid: 4909e413-f3b0-4183-8ad3-67b1434df742
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4cb3213b6a4c5711ccb8d6f9243047d8361a6e37
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "67925428"
---
# <a name="error-handling"></a>错误处理
ADO 使用多种不同的方法来通知应用程序发生的错误。 本部分讨论在使用 ADO 时可能发生的错误类型以及应用程序的通知方式。 它通过提出有关如何处理这些错误的建议来结束。  
  
## <a name="how-does-ado-report-errors"></a>ADO 如何报告错误？  
 ADO 按多种方式通知错误：  
  
-   ADO 错误生成运行时错误。 像处理任何其他运行时错误一样处理 ADO 错误，如在 Visual Basic 中使用**On error**语句。  
  
-   程序可能会收到来自 OLE DB 的错误。 OLE DB 错误也会生成运行时错误。  
  
-   如果错误特定于您的数据访问接口，则在发生错误时，将一个或多个**错误**对象置于用于访问数据存储的**连接**对象的**错误**集合中。  
  
-   如果引发事件的进程还产生了错误，则会将错误消息放置在**错误**对象中，并将其作为参数传递给事件。 有关事件的详细信息，请参阅[处理 ADO 事件](../../../ado/guide/data/handling-ado-events.md)。  
  
-   处理批处理更新或涉及**记录集**的其他大容量操作时出现的问题可以通过**记录集**的**Status**属性来指示。 例如，可以通过**RecordStatusEnum**值指定架构约束冲突或权限不足。  
  
-   与当前记录中的特定**字段**相关的问题也由**记录**或**记录集**的**字段**集合中每个**字段**的**Status**属性来指示。 例如，无法完成的更新或不兼容的数据类型可以通过**FieldStatusEnum**值来指定。  
  
 本部分包含以下主题。  
  
-   [ADO 错误](../../../ado/guide/data/ado-errors.md)  
  
-   [提供程序错误](../../../ado/guide/data/provider-errors.md)  
  
-   [字段相关错误信息](../../../ado/guide/data/field-related-error-information.md)  
  
-   [记录集相关错误信息](../../../ado/guide/data/recordset-related-error-information.md)  
  
-   [处理其他语言中的处理错误](../../../ado/guide/data/handling-errors-in-other-languages.md)  
  
-   [预测错误](../../../ado/guide/data/anticipating-errors.md)
