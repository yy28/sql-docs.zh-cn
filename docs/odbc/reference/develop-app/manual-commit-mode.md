---
title: 手动提交模式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- rolling back transactions [ODBC]
- manual-commit mode [ODBC]
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
- transactions [ODBC], rolling back
ms.assetid: 9c4b3931-e48b-4960-89a2-5697537e9f51
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7189a0586ba4f62091d5eb209a56931627bc6f7f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036400"
---
# <a name="manual-commit-mode"></a>手动提交模式
*在手动提交模式下，* 应用程序必须显式完成事务，通过调用**SQLEndTran**将它们提交或回滚它们。 这是大多数关系数据库的正常事务模式。  
  
 ODBC 中的事务不需要显式启动。 相反，事务隐式开始将每次应用程序启动对数据库运行时。 如果数据源需要显式事务启动，该驱动程序必须提供它每次应用程序执行需要事务的语句以及没有当前事务时。
