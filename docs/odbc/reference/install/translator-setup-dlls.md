---
title: "转换器安装程序 Dll |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: translator setup DLL [ODBC]
ms.assetid: b3ca79e9-01b9-4541-81de-bbbad24ca736
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3ce6961ec470bf0e0a7281a129d85f5cf69c9b80
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="translator-setup-dlls"></a>转换器安装程序 Dll
> [!NOTE]  
>  从 Windows XP 和 Windows Server 2003 开始，在 Windows 操作系统中包含 ODBC。 在早期版本的 Windows 上，应仅显式安装 ODBC。  
  
 DLL 包含转换器安装**ConfigTranslator**函数，返回一个转换器的默认选项。 如有必要，则会提示用户输入此信息。 此函数的完整说明，请参阅[安装 DLL API 参考](../../../odbc/reference/syntax/setup-dll-api-reference.md)。  
  
 转换器安装程序 DLL 是由转换器开发人员编写的。 它可以是转换器的一部分的 DLL 或单独的 DLL。
