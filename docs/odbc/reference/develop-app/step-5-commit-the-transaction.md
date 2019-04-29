---
title: 步骤 5：提交的事务 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 341f34afa1dbe65f4b83a46f461bb93f4fb4f4c8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63148946"
---
# <a name="step-5-commit-the-transaction"></a>步骤 5：提交事务
下一步是提交事务，如以下插图所示。  
  
 ![演示如何提交的事务](../../../odbc/reference/develop-app/media/pr16.gif "pr16")  
  
 第五个步骤是调用**SQLEndTran**来提交或回滚事务。 在应用程序执行此步骤中，仅当其将事务提交模式设置为手动提交;如果事务提交模式为自动提交，即默认值，执行语句时，将自动提交事务。 有关详细信息，请参阅[事务](../../../odbc/reference/develop-app/transactions-odbc.md)。  
  
 若要在新的事务中执行语句，该应用程序，返回到步骤 3。 若要从数据源断开连接，该应用程序继续执行到步骤 6。
