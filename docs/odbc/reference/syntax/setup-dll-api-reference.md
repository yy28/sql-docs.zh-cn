---
title: 安装程序 DLL API 参考 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ODBC drivers [ODBC], driver setup DLL
- driver setup DLL [ODBC]
ms.assetid: f9d03f17-1c0d-4e7c-9c04-8c316e07ef25
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 33898a338fa93a9088065c116df4f1f46e873657
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="setup-dll-api-reference"></a>安装程序 DLL API 参考
本部分介绍驱动程序安装程序包含两个函数的 DLL API 的语法 (**ConfigDriver**和**ConfigDSN**)。 **ConfigDriver**和**ConfigDSN**可以是驱动程序 DLL 中或在单独的安装程序 DLL。  
  
 此外，本部分介绍转换器安装程序 DLL API，包含单个函数的语法 (**ConfigTranslator**)。 **ConfigTranslator**可以是转换器 DLL 中或在单独的安装程序 DLL。  
  
 每个函数都标有在其中引入的 ODBC 的版本。  
  
 本部分包含以下主题。  
  
-   [ConfigDriver 函数](../../../odbc/reference/syntax/configdriver-function.md)  
  
-   [ConfigDSN 函数](../../../odbc/reference/syntax/configdsn-function.md)  
  
-   [ConfigTranslator 函数](../../../odbc/reference/syntax/configtranslator-function.md)
