---
title: 撤消和授予权限时使用存储过程 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], stored procedures
ms.assetid: 24070039-03ab-4623-a681-6308802eb399
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1ed3fa04ffbb67f0c6ddeba677a411c9c99c4768
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32904132"
---
# <a name="revoking-and-granting-rights-when-using-stored-procedures"></a>撤销和授予权限时使用存储的过程
> [!IMPORTANT]  
>  将 Windows 的未来版本中删除该功能。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 相反，使用提供的 Oracle 的 ODBC 驱动程序。  
  
 在用户权限授予并且然后吊销对存储过程访问表时，Microsoft ODBC Driver for Oracle 将返回以下错误消息：  
  
 SQL_ERROR = 1  
  
 szErrorMsg ="[Microsoft] [适用于 Oracle 的 ODBC 驱动程序] 参数数目不正确"  
  
 szErrorMsg ="[Microsoft] [适用于 Oracle 的 ODBC 驱动程序] 语法错误或访问冲突"  
  
 对 Oracle OCI 函数 Odessp() 的调用在此方案中无法正常工作，但为实现默认参数是必需的。 基础的表权限被修改后，必须再次运行之前重新编译存储的过程。
