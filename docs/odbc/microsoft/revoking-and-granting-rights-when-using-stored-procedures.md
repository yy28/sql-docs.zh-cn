---
title: 撤销和授予权限时使用存储过程 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e881201e4653a168faff2fa438be19c1ca37e9b1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63127968"
---
# <a name="revoking-and-granting-rights-when-using-stored-procedures"></a>使用存储过程时撤销和授予权限
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 相反，使用提供的 Oracle 的 ODBC 驱动程序。  
  
 Microsoft ODBC Driver for Oracle 时的用户权限是授予，然后撤消的对存储过程中访问的表返回以下错误消息：  
  
 SQL_ERROR=-1  
  
 szErrorMsg="[Microsoft][ODBC driver for Oracle]Wrong number of parameters"  
  
 szErrorMsg ="[Microsoft] [Oracle ODBC 驱动程序] 语法错误或访问冲突"  
  
 对 Oracle OCI 函数 Odessp() 的调用在此方案中会失败，但为实现默认参数是必需的。 基础表权限被修改后，必须再次运行前重新编译存储的过程。
