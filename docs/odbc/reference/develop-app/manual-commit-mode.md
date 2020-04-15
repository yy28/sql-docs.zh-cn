---
title: 手动提交模式 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2a00ff373e374d0940b3e7259eeb01e26b620cae
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287871"
---
# <a name="manual-commit-mode"></a>手动提交模式
*在手动提交模式下，* 应用程序必须通过调用**SQLEndTran**来显式完成事务，以提交它们或回滚它们。 这是大多数关系数据库的正常事务模式。  
  
 ODBC 中的事务不必显式启动。 相反，每当应用程序开始在数据库上运行时，事务都会隐式启动。 如果数据源需要显式事务启动，则每当应用程序执行需要事务的语句并且没有当前事务时，驱动程序必须提供它。
