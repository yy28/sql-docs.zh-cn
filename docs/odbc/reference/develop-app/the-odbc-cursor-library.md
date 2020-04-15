---
title: ODBC 光标库 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], about cursor library
- ODBC cursor library [ODBC]
- cursor library [ODBC], about cursor library
- scrollable cursors [ODBC]
- cursors [ODBC], cursor library
- block cursors [ODBC]
ms.assetid: 32fb7df0-953a-4f68-b041-7d2852e45d0f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b243e8ae2dc931830a249d4392da308e68722cdf
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300047"
---
# <a name="the-odbc-cursor-library"></a>ODBC 游标库
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的光标功能。  
  
 块和可滚动游标是许多应用程序的非常有用的附加功能。 但是，并非所有驱动程序都支持块和可滚动的游标。 定位更新和删除语句和**SQLSetPos**也是如此，在更新数据中讨论。 因此，以前包含在 Microsoft 数据访问组件 （MDAC） SDK 中的 Windows SDK 的 ODBC 组件包括游标库。 游标库为满足开放组标准 CLI 一致性级别的任何驱动程序实现块、静态游标、定位更新和删除语句以及**SQLSetPos。** 游标库可以与 ODBC 应用程序重新分发;有关详细信息，请参阅 SDK 中的许可协议。  
  
 要使用游标库，应用程序在连接到数据源之前设置SQL_ATTR_ODBC_CURSORS连接属性。 有关游标库的详细信息，请参阅附录[F：ODBC 游标库](../../../odbc/reference/appendixes/appendix-f-odbc-cursor-library.md)。
