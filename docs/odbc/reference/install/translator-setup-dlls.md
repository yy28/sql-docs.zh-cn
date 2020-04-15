---
title: 转换器设置 DLL |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 28c354fddb36b9e035361fa4ba03fbde34b7d399
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296047"
---
# <a name="translator-setup-dlls"></a>转换器安装程序 DLL
> [!NOTE]  
>  从 Windows XP 和 Windows 服务器 2003 开始，ODBC 包含在 Windows 操作系统中。 您只应在早期版本的 Windows 上显式安装 ODBC。  
  
 转换器设置 DLL 包含 **"配置转换器"** 功能，该函数返回转换器的默认选项。 如有必要，它会提示用户获得此信息。 有关此功能的完整说明，请参阅[设置 DLL API 参考](../../../odbc/reference/syntax/setup-dll-api-reference.md)。  
  
 翻译器设置 DLL 由翻译开发人员编写。 它可以是转换器 DLL 的一部分，也可以是单独的 DLL。
