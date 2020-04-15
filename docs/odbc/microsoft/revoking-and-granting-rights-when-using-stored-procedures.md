---
title: 使用存储过程时撤销和授予权限 |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303983"
---
# <a name="revoking-and-granting-rights-when-using-stored-procedures"></a>使用存储过程时撤销和授予权限
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 而是使用 Oracle 提供的 ODBC 驱动程序。  
  
 当授予用户权限然后在存储过程访问的表上撤消时，Oracle 的 Microsoft ODBC 驱动程序将返回以下错误消息：  
  
 SQL_ERROR=-1  
  
 szErrorMsg_"[微软][Oracle的ODBC驱动程序]错误数量的参数"  
  
 szErrorMsg_"[微软][Oracle的ODBC驱动程序]语法错误或访问冲突"  
  
 在这种情况下，对 Oracle OCI 函数 Odessp（） 的调用失败，但为了实现默认参数是必要的。 修改基础表权限后，必须先重新编译存储过程，然后再运行它。
