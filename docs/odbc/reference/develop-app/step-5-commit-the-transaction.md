---
description: 步骤 5：提交事务
title: 步骤5：提交事务 |Microsoft Docs
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
ms.openlocfilehash: b4cc3a73e5cfc564992795ab6b18759b1066288c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88385893"
---
# <a name="step-5-commit-the-transaction"></a>步骤 5：提交事务
下一步是提交事务，如下图所示。  
  
 ![显示如何提交事务](../../../odbc/reference/develop-app/media/pr16.gif "pr16")  
  
 第五步是调用 **SQLEndTran** 来提交或回滚事务。 仅当应用程序将事务提交模式设置为手动提交时，应用程序才会执行此步骤;如果事务提交模式为自动提交（这是默认值），则执行语句时，将自动提交事务。 有关详细信息，请参阅[事务](../../../odbc/reference/develop-app/transactions-odbc.md)。  
  
 若要在新事务中执行语句，应用程序会返回到步骤3。 若要断开与数据源的连接，应用程序将继续执行步骤6。
