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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a85868cf22fa6d385c3bf75261e0f1cd54e4e1d0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63149085"
---
# <a name="the-odbc-cursor-library"></a>ODBC 游标库
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 避免在新的开发工作中使用此功能并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 块和可滚动游标是许多应用程序的非常有用附加工具。 但是，并非所有驱动程序支持块和可滚动游标。 相同的定位更新和删除语句和**SQLSetPos**，论述了更新的数据中。 因此，以前包含在 Microsoft 数据访问组件 (MDAC) SDK，Windows SDK 的 ODBC 组件包括游标库。 游标库实现块、 静态游标、 定位的 update 和 delete 语句，并**SQLSetPos**满足打开组标准 CLI 的一致性级别的任何驱动程序。 游标库可以与 ODBC 应用程序; 再分发请参阅 SDK for 的详细信息中的许可协议。  
  
 若要使用游标库，应用程序设置 SQL_ATTR_ODBC_CURSORS 连接属性之后才会连接到数据源。 有关游标库的详细信息，请参阅[附录 f:ODBC 游标库](../../../odbc/reference/appendixes/appendix-f-odbc-cursor-library.md)。
