---
title: 模块和起始 (XQuery) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql
ms.component: xquery
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- XQuery, prolog
- prolog
ms.assetid: 0f17b4a4-6234-41d4-a996-6db4e27bff7e
caps.latest.revision: 13
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 08d19f2a24c243647b4004a557fd25bf96d2dd62
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="modules-and-prologs-xquery"></a>模块和 Prolog (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [XQuery Prolog](../xquery/modules-and-prologs-xquery-prolog.md)是一系列的命名空间声明。 在 Prolog 中使用声明命名空间时，可以为命名空间绑定指定前缀并在查询正文中使用该前缀。  
  
## <a name="implementation-limitations"></a>实现限制  
 在此实现中，不支持下列 XQuery 规范：  
  
-   模块声明 (`version`)  
  
-   模块声明 (`module namespace`)  
  
-   Xmpspacedeclaration (`xmlspace`)  
  
-   默认排序规则声明 (`declare default collation`)  
  
-   基准 URI 声明 (`declare base-uri`)  
  
-   构造声明 (`declare construction`)  
  
-   默认排序声明 (`declare ordering`)  
  
-   架构导入 (`import schema namespace`)  
  
-   模块导入 (`import module`)  
  
-   Prolog 中的变量声明 (`declare variable`)  
  
-   函数声明 (`declare function`)  
  
## <a name="in-this-section"></a>本節內容  
 [XQuery Prolog](../xquery/modules-and-prologs-xquery-prolog.md)  
 介绍 XQuery Prolog。  
  
## <a name="see-also"></a>另请参阅  
 [XQuery 语言参考 (SQL Server)](../xquery/xquery-language-reference-sql-server.md)  
  
  
