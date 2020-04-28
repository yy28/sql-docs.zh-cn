---
title: 驱动程序安装程序 DLL |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306418"
---
# <a name="driver-setup-dll"></a>驱动程序安装程序 DLL
> [!NOTE]  
>  从 Windows XP 和 Windows Server 2003 开始，ODBC 包含在 Windows 操作系统中。 只应在早期版本的 Windows 上显式安装 ODBC。  
  
 驱动程序安装程序 DLL 包含**ConfigDriver**和**ConfigDSN**函数。 **ConfigDriver**执行特定于驱动程序的安装任务，如将驱动程序特定的信息输入注册表。 **ConfigDSN**维护有关注册表中的数据源的特定于驱动程序的信息。 有关这些函数的完整说明，请参阅[安装程序 DLL API 参考](../../../odbc/reference/syntax/setup-dll-api-reference.md)。  
  
 **ConfigDSN**调用安装程序 DLL 中的以下函数，以便在注册表中维护数据源信息：  
  
-   **SQLWriteDSNToIni**。 添加一个数据源。  
  
-   **SQLRemoveDSNFromIni**。 删除数据源。  
  
-   **SQLWritePrivateProfileString**。 在数据源规范子项下编写驱动程序特定的值。  
  
-   **SQLGetPrivateProfileString**。 从数据源规范子项中读取驱动程序特定的值。  
  
-   **SQLGetTranslator**。 提示用户输入转换器名称和选项。 此函数在转换器安装程序 DLL 中调用**ConfigTranslator** 。  
  
 驱动程序安装程序 DLL 由驱动程序开发人员编写。 它可以是驱动程序 DLL 的一部分，也可以是单独的 DLL。
