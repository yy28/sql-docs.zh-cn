---
title: 致电 SQLGetDiagField |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application upgrades [ODBC], SQLGetDiagField
- backward compatibility [ODBC], SqlGetDiagField
- upgrading applications [ODBC], SQLGetDiagField
- SQLGetDiagField function [ODBC], calling
- compatibility [ODBC], SQLGetDiagField
ms.assetid: 3c4fb606-b81c-4f11-9820-f0a54e3bc401
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a097cbdd74cfcd76d2b102bb71dfccb974906709
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306258"
---
# <a name="calling-sqlgetdiagfield"></a>调用 SQLGetDiagField
当 ODBC *3.x*应用程序在 ODBC *2.x*驱动程序中调用**SQLGetDiagField**时，如果*DiagInfoPtr* SQL_DIAG_CLASS_ORIGIN、SQL_DIAG_CLASS_SUBCLASS_ORIGIN、SQL_DIAG_CONNECTION_NAME、SQL_DIAG_MESSAGE_TEXT、SQL_DIAG_NATIVE、SQL_DIAG_NUMBER、SQL_DIAG_RETURNCODE、SQL_DIAG_SERVER_NAME或SQL_DIAG_SQLSTATE，则驱动程序将在*\*DiagInfoPtr*中返回SQL_SUCCESS和相应的信息。 所有其他诊断字段将返回SQL_ERROR。
