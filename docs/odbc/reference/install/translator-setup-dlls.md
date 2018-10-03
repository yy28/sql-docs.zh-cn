---
title: 转换器安装程序 Dll |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- translator setup DLL [ODBC]
ms.assetid: b3ca79e9-01b9-4541-81de-bbbad24ca736
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 20453b792ed00b388977fefe3064fd8dfca86147
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47610125"
---
# <a name="translator-setup-dlls"></a>转换器安装程序 DLL
> [!NOTE]  
>  从 Windows XP 和 Windows Server 2003 开始，ODBC 包括在 Windows 操作系统中。 在早期版本的 Windows 上，应仅显式安装 ODBC。  
  
 转换器安装程序 DLL 包含**ConfigTranslator**函数，返回的默认选项为转换器。 如有必要，它会提示用户输入此信息。 此函数的完整说明，请参阅[安装程序 DLL API 参考](../../../odbc/reference/syntax/setup-dll-api-reference.md)。  
  
 转换器安装程序 DLL 是由转换器开发人员编写的。 也可以是转换器的一部分的 DLL 或单独的 DLL。
