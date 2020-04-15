---
title: 驱动程序设置 DLL |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- installing ODBC components [ODBC], driver setup DLL
- ODBC drivers [ODBC], driver setup DLL
- driver setup DLL [ODBC]
ms.assetid: 49bab021-81fa-402e-b7a4-a5214f1fadc4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a0a2878591c92fe0b2070a295d9dc622c245c17e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306418"
---
# <a name="driver-setup-dll"></a>驱动程序安装程序 DLL
> [!NOTE]  
>  从 Windows XP 和 Windows 服务器 2003 开始，ODBC 包含在 Windows 操作系统中。 您只应在早期版本的 Windows 上显式安装 ODBC。  
  
 驱动程序设置 DLL 包含**配置驱动程序**和**配置DSN**功能。 **ConfigDriver**执行特定于驱动程序的安装任务，例如将特定于驱动程序的信息输入注册表。 **配置DSN**维护有关注册表中数据源的特定于驱动程序的信息。 有关这些功能的完整说明，请参阅设置[DLL API 参考](../../../odbc/reference/syntax/setup-dll-api-reference.md)。  
  
 **ConfigDSN**调用安装程序 DLL 中的以下函数来维护注册表中的数据源信息：  
  
-   **SQLwriteSntoini**. 添加一个数据源。  
  
-   **SQLremoveSnfromini**。 删除数据源。  
  
-   **SQLWrite私有配置文件字符串**。 在数据源规范子键下编写特定于驱动程序的值。  
  
-   **SQLGet私人配置文件字符串**。 从数据源规范子键读取特定于驱动程序的值。  
  
-   **SQLGet 翻译器**。 提示用户输入翻译人员姓名和选项。 此函数在转换器设置 DLL 中调用**配置转换器**。  
  
 驱动程序设置 DLL 由驱动程序开发人员编写。 它可以是驱动程序 DLL 的一部分，也可以是单独的 DLL。
