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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: df91638f91091940e00e7a6a19d0fd6cb700f85f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68094164"
---
# <a name="driver-setup-dll"></a>驱动程序安装程序 DLL
> [!NOTE]  
>  从 Windows XP 和 Windows Server 2003 开始，ODBC 包括在 Windows 操作系统中。 在早期版本的 Windows 上，应仅显式安装 ODBC。  
  
 驱动程序安装程序 DLL 包含**ConfigDriver**并**ConfigDSN**函数。 **ConfigDriver**执行特定于驱动程序的安装任务，例如输入到注册表的特定于驱动程序的信息。 **ConfigDSN**会维护有关在注册表中的数据源的特定于驱动程序的信息。 有关这些函数的完整说明，请参阅[安装程序 DLL API 参考](../../../odbc/reference/syntax/setup-dll-api-reference.md)。  
  
 **ConfigDSN**安装程序来维护注册表中的数据源信息的 DLL 中调用以下函数：  
  
-   **SQLWriteDSNToIni**。 添加数据源。  
  
-   **SQLRemoveDSNFromIni**。 删除数据源。  
  
-   **SQLWritePrivateProfileString**。 写入数据源规范子项下的特定于驱动程序的值。  
  
-   **不到 SQLGetPrivateProfileString**。 从数据源规范子项读取特定于驱动程序的值。  
  
-   **SQLGetTranslator**。 提示用户输入的转换器名称和选项。 此函数将调用**ConfigTranslator**转换器安装程序 DLL。  
  
 驱动程序安装程序 DLL 是由驱动程序开发人员编写的。 它可以是驱动程序的一部分的 DLL 或单独的 DLL。
