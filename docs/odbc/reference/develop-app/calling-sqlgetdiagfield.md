---
title: 调用 SQLGetDiagField |Microsoft 文档
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
- application upgrades [ODBC], SQLGetDiagField
- backward compatibility [ODBC], SqlGetDiagField
- upgrading applications [ODBC], SQLGetDiagField
- SQLGetDiagField function [ODBC], calling
- compatibility [ODBC], SQLGetDiagField
ms.assetid: 3c4fb606-b81c-4f11-9820-f0a54e3bc401
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5b89a561623001091bb3e03cce0b47c59d25493c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="calling-sqlgetdiagfield"></a>调用 SQLGetDiagField
当一个 ODBC 3。*x*应用程序调用**SQLGetDiagField** ODBC 2 中 *.x*驱动程序，该驱动程序将返回 SQL_SUCCESS 和中的相应信息 *\*DiagInfoPtr*如果*DiagIdentifier*自变量是 SQL_DIAG_CLASS_ORIGIN、 SQL_DIAG_CLASS_SUBCLASS_ORIGIN、 SQL_DIAG_CONNECTION_NAME、 SQL_DIAG_MESSAGE_TEXT、 SQL_DIAG_NATIVE、 SQL_DIAG_数、 SQL_DIAG_RETURNCODE、 SQL_DIAG_SERVER_NAME 或 SQL_DIAG_SQLSTATE。 诊断的所有其他字段将返回 SQL_ERROR。
