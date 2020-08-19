---
description: ODBC 静态游标
title: ODBC 静态游标 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], static
- static cursors [ODBC]
ms.assetid: 28cb324c-e1c3-4b5c-bc3e-54df87037317
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9689badd39e21f82c268be904b29ffb1fa90a8ae
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429159"
---
# <a name="odbc-static-cursors"></a>ODBC 静态游标
静态游标是结果集看似静态的游标。 它通常不会检测在打开游标后对结果集的成员资格、顺序或值所做的更改。 例如，假定静态游标提取行，另一个应用程序随后更新该行。 如果静态游标 refetches 行，则它看到的值将保持不变，尽管其他应用程序所做的更改。  
  
 静态游标可以检测自己的更新、删除和插入操作，尽管不需要执行此操作。 特定静态游标是否检测这些更改通过 **SQLGetInfo**中的 SQL_STATIC_SENSITIVITY 选项进行报告。 静态游标从不检测其他更新、删除和插入操作。  
  
 SQL_ATTR_ROW_STATUS_PTR 语句特性指定的行状态数组可以包含任意行的 SQL_ROW_SUCCESS、SQL_ROW_SUCCESS_WITH_INFO 或 SQL_ROW_ERROR。 它为游标更新、删除或插入的行返回 SQL_ROW_UPDATED、SQL_ROW_DELETED 或 SQL_ROW_ADDED，假设游标可以检测到此类更改。  
  
 通常通过锁定结果集中的行或通过生成结果集的副本或快照来实现静态游标。 虽然锁定行相对简单，但它具有明显降低并发性的缺点。 通过创建复制，可以更好地进行并发，并允许光标通过修改副本来跟踪自己的更新、删除和插入。 但是，复制的开销更高，并且可与基础数据分离，因为其他人更改了数据。
