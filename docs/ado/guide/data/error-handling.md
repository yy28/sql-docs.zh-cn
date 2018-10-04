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
manager: craigg
ms.openlocfilehash: 5d8f96b28a15258df4b7d093ce14f227f28ad9b0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47633511"
---
# <a name="error-handling"></a>错误处理
ADO 使用多种不同的方法来通知发生的错误的应用程序。 本部分介绍使用 ADO 和如何通知您的应用程序时可能发生的错误的类型。 最后，它提出有关如何处理这些错误的建议。  
  
## <a name="how-does-ado-report-errors"></a>ADO 如何报告错误？  
 ADO 会通知你通过多种方法中的错误：  
  
-   ADO 错误会生成运行时错误。 像任何其他运行时错误，例如，使用相同的方式处理 ADO 错误**On Error**在 Visual Basic 中的语句。  
  
-   您的程序可以接收来自 OLE DB 错误。 OLE DB 错误生成了的运行时错误。  
  
-   如果错误是特定于数据访问接口，一个或多个**错误**对象都将置于**错误**的集合**连接**对象，用于访问数据存储区中出现错误。  
  
-   如果引发事件的进程也产生了错误，错误信息置于**错误**对象，并作为参数传递给该事件。 请参阅[处理 ADO 事件](../../../ado/guide/data/handling-ado-events.md)有关事件的详细信息。  
  
-   处理过程中发生的问题批处理更新或其他大容量操作涉及**记录集**可以为由**状态**属性**记录集**。 例如，通过指定架构约束冲突或没有足够的权限**RecordStatusEnum**值。  
  
-   发生涉及特定的问题**字段**由还指示当前记录**状态**每个属性**字段**中**字段**的集合**记录**或**记录集**。 例如，通过指定不兼容的数据类型或无法完成的更新**FieldStatusEnum**值。  
  
 本部分包含以下主题。  
  
-   [ADO 错误](../../../ado/guide/data/ado-errors.md)  
  
-   [提供程序错误](../../../ado/guide/data/provider-errors.md)  
  
-   [字段相关错误信息](../../../ado/guide/data/field-related-error-information.md)  
  
-   [记录集相关错误信息](../../../ado/guide/data/recordset-related-error-information.md)  
  
-   [处理其他语言中的处理错误](../../../ado/guide/data/handling-errors-in-other-languages.md)  
  
-   [预测错误](../../../ado/guide/data/anticipating-errors.md)
