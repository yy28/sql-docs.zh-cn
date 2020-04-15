---
title: 设置扩展安西SQL |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- extendedANSISQL [ODBC], setting
ms.assetid: 37b775d1-65ac-45ac-8572-454bc4e3c1a2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6b5c2e4ed4d8bd64d02fb6a62861db832f6b0898
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300797"
---
# <a name="setting-extendedansisql"></a>设置 ExtendedAnsiSQL
可以通过添加扩展 AnsiSQL 属性在连接字符串中控制该属性：  
  
|“值”|描述|  
|-----------|-----------------|  
|扩展安西SQL=0（默认）|此设置无法启用新功能。|  
|扩展安西SQL_1|此设置启用新功能。|  
  
 在通过控制面板配置 DSN 时，还可以通过 **"高级选项"** 对话框在 DSN 中设置该属性。  
  
 将属性设置为 0 会禁用新功能;将其设置为 1 启用新功能。  
  
 也可以使用 SQLSetConnectAttr（） 设置该属性。 属性值为 65501，并设置为 SQLINTEGER 值 1 或 0，如上表所述。 它可以在连接之前或之后调用，但最好在连接后调用它，因为驱动程序处理缓存的连接属性和连接字符串的顺序。
