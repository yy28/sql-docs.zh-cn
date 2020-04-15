---
title: 设置描述符字段 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], retrieving or setting field values
ms.assetid: d735dc64-370f-48ab-a59f-6cef9bc4e1e8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 04f9520e2ef462df481bb104e389aeb57b5dd457
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304148"
---
# <a name="setting-descriptor-fields"></a>设置描述符字段
要修改描述符的字段，应用程序可以调用**SQLSetDescField**。 某些字段是只读的，无法设置。 （请参阅[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)函数说明。  
  
 描述符记录字段的设置记录编号 （*RecNumber*） 为 1 或更高，而描述符标头字段的设置记录数为 0。 记录数为 0 也用于设置书签字段，根据第 0 列中包含的书签的约定。 这可能会给人留下书签字段包含在描述符标头中的印象，但事实并非如此。 书签字段与标题字段不同。  
  
 单独设置字段时，应用程序应遵循[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)中定义的顺序。 设置某些字段会导致驱动程序设置其他字段。 这可确保描述符始终准备好在应用程序指定数据类型后使用。 当应用程序设置SQL_DESC_TYPE字段时，驱动程序会检查指定类型的其他字段是否有效且一致。  
  
 如果将设置描述符字段的函数调用失败，则描述符字段的内容在函数调用失败后未定义。
