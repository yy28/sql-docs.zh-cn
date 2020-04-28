---
title: 使用存储过程时撤消和授予权限 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], stored procedures
ms.assetid: 24070039-03ab-4623-a681-6308802eb399
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 469e6f0fdc6794e3bd163844e43821798aa4a617
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303983"
---
# <a name="revoking-and-granting-rights-when-using-stored-procedures"></a>使用存储过程时撤销和授予权限
> [!IMPORTANT]  
>  此功能将在 Windows 的将来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 请改用 Oracle 提供的 ODBC 驱动程序。  
  
 当在存储过程访问的表上授予或撤销用户权限时，适用于 Oracle 的 Microsoft ODBC 驱动程序将返回以下错误消息：  
  
 SQL_ERROR =-1  
  
 szErrorMsg = "[Microsoft] [用于 Oracle 的 ODBC 驱动程序] 参数的数目不正确"  
  
 szErrorMsg = "[Microsoft] [ODBC driver for Oracle] 语法错误或访问冲突"  
  
 在这种情况下，对 Oracle OCI function Odessp （）的调用将失败，但必须要实现默认参数。 修改基础表权限之后，必须重新编译该存储过程，然后再次运行该存储过程。
