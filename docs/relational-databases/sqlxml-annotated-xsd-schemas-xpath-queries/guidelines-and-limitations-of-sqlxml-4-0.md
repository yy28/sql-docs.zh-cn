---
title: SQLXML 4.0 的准则和限制 |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXML, about SQLXML
ms.assetid: fe433d30-90a1-421e-85c6-af13294dc18d
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 411495986ed700a069a7c8124a7d0829102138fe
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68073367"
---
# <a name="guidelines-and-limitations-of-sqlxml-40"></a>SQLXML 4.0 的准则和限制
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  使用 SQLXML 4.0 时请记住以下事项：  
  
-   不针对生成 XML 的映射架构验证作为查询结果返回的 XML。  
  
-   SQLXML 4.0 既包括与版本无关的 PROGID，也包括与版本相关的 PROGID。 建议所有生产应用程序都使用与版本相关的 PROGID。 由于 SQLXML 4.0 不完全向后兼容，这一点尤其重要。 只有使用与版本相关的 PROGID，在安装较新版本时，才能保证您的应用程序可继续工作，而不会失败。 不同版本的程序行为可能出于多种原因（如错误修复、可能的设计更改等）而有所变化。 使用与版本相关的 PROGID 可防止在安装较新版本时出现意外失败。 使用与版本相关的 PROGID 安装较新版本时，您的应用程序将继续工作，而不会失败。 如果决定更改以前的与版本相关的 PROGID，转而使用较新版本中最近的与版本相关的 PROGID，您必须在投入使用前测试您的应用程序。 例如，使用与版本无关的 PROGID 的应用程序将在以下情况下失败：  
  
     正在运行使用 SQLXML 4.0 和与版本无关的 PROGID 的应用程序，而且您决定安装其他某种软件程序。 此程序可能安装较早版本的 SQLXML。 由于您的应用程序中的与版本无关的 PROGID 现在指向较早版本的 SQLXML（其中可能具有或不具有您的应用程序正在使用的 SQLXML 功能），您的应用程序可能失败。  
  
-   如果出于任何原因不想要使用 sqlxmloledb 访问接口，并改为想要使用 SQLOLEDB 的 SQLXML 功能的提供程序设置**SQLXML Version**属性设置为"SQLXML.4.0"。  
  
  
