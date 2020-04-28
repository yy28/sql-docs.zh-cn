---
title: ODBC 游标库 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300047"
---
# <a name="the-odbc-cursor-library"></a>ODBC 游标库
> [!IMPORTANT]  
>  此功能将在 Windows 的将来版本中删除。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 块和可滚动游标对于许多应用程序来说非常有用。 但是，并非所有驱动程序都支持块游标和可滚动游标。 这同样适用于更新数据的定位更新和删除语句和**SQLSetPos**。 因此，Windows SDK 的 ODBC 组件（以前包含在 Microsoft 数据访问组件（MDAC） SDK 中）包含一个游标库。 游标库实现块、静态游标、定位更新和删除语句，并为满足开放组标准 CLI 一致性级别的任何驱动程序实现**SQLSetPos** 。 可以在 ODBC 应用程序中重新分发游标库;有关详细信息，请参阅 SDK 中的许可协议。  
  
 若要使用游标库，应用程序会在连接到数据源之前设置 SQL_ATTR_ODBC_CURSORS 连接属性。 有关游标库的详细信息，请参阅[附录 F： ODBC 游标库](../../../odbc/reference/appendixes/appendix-f-odbc-cursor-library.md)。
