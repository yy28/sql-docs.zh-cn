---
title: SQLSetEnvAttr 和光标库 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetEnvAttr function [ODBC], Cursor Library
ms.assetid: 59cc8eae-09ae-4796-869a-c5806488ae83
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 42d6804bf8a3544de44c03266ce28712e1b04d90
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300517"
---
# <a name="sqlsetenvattr-and-the-cursor-library"></a>SQLSetEnvAttr 和游标库
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的光标功能。  
  
 本主题讨论使用**SQLSetEnvAttr**函数与游标库。 有关**SQLSetEnvAttr 的**一般信息，请参阅[SQLSetEnvAttr 函数](../../../odbc/reference/syntax/sqlsetenvattr-function.md)。  
  
 无论应用程序版本或驱动程序版本如何，游标库不受SQL_ATTR_ODBC_VERSION环境属性设置的影响。
