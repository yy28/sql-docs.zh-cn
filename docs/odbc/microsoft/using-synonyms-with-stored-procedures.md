---
title: 将同义词与存储过程一起使用 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], stored procedures
ms.assetid: 8620b039-a086-4534-8710-cc8b1787dc80
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6d3758aeb954427f333c5a22298d6675c04acdb5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292757"
---
# <a name="using-synonyms-with-stored-procedures"></a>在存储过程中使用同义词
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 而是使用 Oracle 提供的 ODBC 驱动程序。  
  
 调用 Oracle 存储过程时，Oracle 版本 2.0 和 2.5 的 Microsoft ODBC 驱动程序不支持同义词。 当与其他 Oracle 数据库对象（如表）一起使用时，同义词按预期工作。
