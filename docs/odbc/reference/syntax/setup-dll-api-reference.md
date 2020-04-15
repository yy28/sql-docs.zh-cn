---
title: 设置 DLL API 参考 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], driver setup DLL
- driver setup DLL [ODBC]
ms.assetid: f9d03f17-1c0d-4e7c-9c04-8c316e07ef25
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 25cff50b73868b5b3015dfc1a00c560c344a6d36
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298882"
---
# <a name="setup-dll-api-reference"></a>Setup DLL API 函数
本节介绍驱动程序设置 DLL API 的语法，它由两个函数（**配置驱动程序**和**配置DSN）** 组成。 **配置驱动程序**和**配置DSN**可以位于驱动程序 DLL 中，也可以位于单独的设置 DLL 中。  
  
 此外，本节还介绍译者设置 DLL API 的语法，该 API 由单个函数（**配置转换器**）组成。 **配置转换器**可以位于转换器 DLL 中，也可以位于单独的设置 DLL 中。  
  
 每个函数都标有引入该函数的 ODBC 版本。  
  
 本部分包含以下主题。  
  
-   [ConfigDriver 函数](../../../odbc/reference/syntax/configdriver-function.md)  
  
-   [ConfigDSN 函数](../../../odbc/reference/syntax/configdsn-function.md)  
  
-   [ConfigTranslator 函数](../../../odbc/reference/syntax/configtranslator-function.md)
