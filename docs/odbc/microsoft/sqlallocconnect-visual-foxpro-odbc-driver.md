---
title: SQLAllocConnect （Visual FoxPro ODBC 驱动程序） |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLAllocConnect function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 70d48b12-def5-475c-b8e1-654a55fdfe0f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c7edefc6e5fcda420bb966f93aba8b15e20d1bd9
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="sqlallocconnect-visual-foxpro-odbc-driver"></a>SQLAllocConnect （Visual FoxPro ODBC 驱动程序）
> [!NOTE]  
>  本主题包含 Visual FoxPro ODBC 驱动程序相关的信息。 有关此函数的常规信息，请参阅下的相应主题[ODBC API 参考](../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 支持： 完整  
  
 ODBC API 一致性： 核心级别  
  
 连接句柄，分配内存*hdbc*，由标识环境中*henv*。 驱动程序管理器处理此调用，并调用驱动程序的**SQLAllocConnect**每当[SQLConnect](../../odbc/microsoft/sqlconnect-visual-foxpro-odbc-driver.md)， **SQLBrowseConnect**，或[SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)调用。  
  
 有关详细信息，请参阅[SQLAllocConnect](../../odbc/reference/syntax/sqlallocconnect-function.md)中*ODBC 程序员参考*。
