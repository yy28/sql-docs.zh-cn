---
description: 在存储过程中使用同义词
title: 将同义词用于存储过程 |Microsoft Docs
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
ms.openlocfilehash: 6c0f210aad903dec6b29df2ca1bd121b569c4335
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471299"
---
# <a name="using-synonyms-with-stored-procedures"></a>在存储过程中使用同义词
> [!IMPORTANT]  
>  此功能将在 Windows 的将来版本中删除。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 请改用 Oracle 提供的 ODBC 驱动程序。  
  
 Microsoft ODBC Driver for Oracle 版本2.0 和2.5 在调用 Oracle 存储过程时不支持同义词。 当同义词与其他 Oracle 数据库对象（如表）一起使用时，同义词会按预期方式工作。
