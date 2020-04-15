---
title: 第 5 步：提交事务 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application process [ODBC], committing transactions
- committing transactions [ODBC]
- transaction commit [ODBC]
ms.assetid: 311685e2-f7b5-4ddc-8020-59380cd2f035
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e348ce697e512f30db46d14535cf19bd6d530f61
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283347"
---
# <a name="step-5-commit-the-transaction"></a>步骤 5：提交事务
下一步是提交事务，如下图所示。  
  
 ![显示如何提交事务](../../../odbc/reference/develop-app/media/pr16.gif "pr16")  
  
 第五步是调用**SQLEndTran**提交或回滚事务。 仅当应用程序将事务提交模式设置为手动提交时，应用程序才会执行此步骤;如果事务提交模式是自动提交（默认值），则在执行语句时会自动提交事务。 有关详细信息，请参阅[事务](../../../odbc/reference/develop-app/transactions-odbc.md)。  
  
 要在新事务中执行语句，应用程序将返回到步骤 3。 要断开与数据源的连接，应用程序将继续执行步骤 6。
