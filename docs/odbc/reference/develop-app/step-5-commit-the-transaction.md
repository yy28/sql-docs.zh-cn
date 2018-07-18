---
title: 步骤 5： 提交事务 |Microsoft 文档
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
- application process [ODBC], committing transactions
- committing transactions [ODBC]
- transaction commit [ODBC]
ms.assetid: 311685e2-f7b5-4ddc-8020-59380cd2f035
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a311752588742df8f597ce2957c6ba600d8b47c4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32914732"
---
# <a name="step-5-commit-the-transaction"></a>步骤 5： 提交事务
下一步是提交该事务，如下面的插图中所示。  
  
 ![演示如何以提交事务](../../../odbc/reference/develop-app/media/pr16.gif "pr16")  
  
 第五个步骤是调用**SQLEndTran**无法提交或回滚事务。 在应用程序执行此步骤，只有当它设置为手动提交; 的事务提交模式如果事务提交模式是自动提交，这是默认值，，执行语句时，会自动提交事务。 有关详细信息，请参阅[事务](../../../odbc/reference/develop-app/transactions-odbc.md)。  
  
 若要在新的事务中执行语句，在应用程序，返回到步骤 3。 从数据源断开连接、 应用程序将继续到步骤 6。
