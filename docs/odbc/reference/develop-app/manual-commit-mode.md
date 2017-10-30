---
title: "手动提交模式 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- rolling back transactions [ODBC]
- manual-commit mode [ODBC]
- transactions [ODBC], commit modes
- committing transactions [ODBC]
- commit modes [ODBC]
- transactions [ODBC], rolling back
ms.assetid: 9c4b3931-e48b-4960-89a2-5697537e9f51
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1a5f9d510d1a92ce8faf4fe29f3274afdba6f83b
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="manual-commit-mode"></a>手动提交模式
*在手动提交模式下，*应用程序必须显式完成事务，通过调用**SQLEndTran**无法提交或回滚它们。 这是大多数关系数据库的正常的事务模式。  
  
 ODBC 中的事务不需要显式启动。 相反，事务隐式开始将每次应用程序启动数据库上运行时。 如果数据源需要显式事务启动，该驱动程序必须提供它每次应用程序执行需要事务的语句和没有任何当前事务时。

