---
title: 模块和 Prolog （XQuery） |Microsoft Docs
description: 了解在 XQuery prolog 中声明命名空间时不支持哪些规范。
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- XQuery, prolog
- prolog
ms.assetid: 0f17b4a4-6234-41d4-a996-6db4e27bff7e
author: rothja
ms.author: jroth
ms.openlocfilehash: c7d982e8c944ff1c596dfa4178ce613ec3be709e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85759494"
---
# <a name="modules-and-prologs-xquery"></a>模块和 Prolog (XQuery)
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  [XQuery Prolog](../xquery/modules-and-prologs-xquery-prolog.md)是一系列命名空间声明。 在 Prolog 中使用声明命名空间时，可以为命名空间绑定指定前缀并在查询正文中使用该前缀。  
  
## <a name="implementation-limitations"></a>实现限制  
 在此实现中，不支持下列 XQuery 规范：  
  
-   模块声明 (`version`)  
  
-   模块声明 (`module namespace`)  
  
-   Xmpspacedeclaration （ `xmlspace` ）  
  
-   默认排序规则声明 (`declare default collation`)  
  
-   基准 URI 声明 (`declare base-uri`)  
  
-   构造声明 (`declare construction`)  
  
-   默认排序声明 (`declare ordering`)  
  
-   架构导入 (`import schema namespace`)  
  
-   模块导入 (`import module`)  
  
-   Prolog 中的变量声明 (`declare variable`)  
  
-   函数声明 (`declare function`)  
  
## <a name="in-this-section"></a>本节内容  
 [XQuery Prolog](../xquery/modules-and-prologs-xquery-prolog.md)  
 介绍 XQuery Prolog。  
  
## <a name="see-also"></a>另请参阅  
 [XQuery 语言参考 (SQL Server)](../xquery/xquery-language-reference-sql-server.md)  
  
  
