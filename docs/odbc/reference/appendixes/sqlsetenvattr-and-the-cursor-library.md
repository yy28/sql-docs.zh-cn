---
title: SQLSetEnvAttr 和游标库 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 74e57f98b7d5e3e1508a960b342521ea5d315a3d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63297524"
---
# <a name="sqlsetenvattr-and-the-cursor-library"></a>SQLSetEnvAttr 和游标库
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 避免在新的开发工作中使用此功能并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 本主题介绍如何使用**SQLSetEnvAttr**函数和游标库。 有关常规信息**SQLSetEnvAttr**，请参阅[SQLSetEnvAttr 函数](../../../odbc/reference/syntax/sqlsetenvattr-function.md)。  
  
 游标库不受 SQL_ATTR_ODBC_VERSION 环境特性，而不考虑应用程序版本或驱动程序版本的设置。
