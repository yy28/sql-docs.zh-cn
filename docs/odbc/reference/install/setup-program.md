---
title: "安装程序 |Microsoft 文档"
ms.custom: 
ms.date: 08/31/2016
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: installing ODBC components [ODBC], setup program
ms.assetid: 9cc5d75d-b293-41e5-927c-10f4af2e7af1
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 741ccfc8e9a096b60eca94b125890d48f65eb764
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="setup-program"></a>安装程序
> **注意：**使用 Windows XP 和 Windows Server 2003 中，启动**ODBC 包含在 Windows 操作系统中**。 在早期版本的 Windows 上，应仅显式安装 ODBC。  
  
 用户在运行安装程序启动安装过程。 安装程序编写的应用程序或驱动程序开发人员。 除了安装 ODBC 组件，它可以安装其他软件。 例如，应用程序开发人员可能使用相同的安装程序来安装 ODBC 组件并安装其应用程序。  
  
 开发人员可以从头开始编写安装程序，使用 Microsoft® Windows® SDK 安装程序工具或其他供应商的安装程序软件。 这样，这些开发人员对安装程序的外观和感觉的完全控制。 可以编写安装程序以安装其他软件，如 ODBC 应用程序。 Windows SDK 安装程序实用工具的详细信息，请参阅 Windows SDK 文档。  
  
 安装中有多少实际上可通过安装程序依赖于它在安装程序 DLL 的调用哪些函数。 安装程序 DLL 包含用于安装各个 ODBC 组件函数。 安装程序只需调用**SQLInstallDriverManager**， **SQLInstallDriverEx**，或**SQLInstallTranslatorEx**在安装程序 DLL，若要检索的路径在其中组件是要安装并向注册表添加有关组件的信息的目录。 这些函数实际上不复制文件;安装程序会尝试使用这些函数的自变量中的信息。  
  
 安装程序 DLL 还包含用于删除 ODBC 组件函数。 在安装程序调用**SQLRemoveDriverManager**， **SQLRemoveDriver**，或**SQLRemoveTranslator** DLL 以降低组件的使用情况计数的在安装程序注册表和组件的新的使用情况计数降为 0，如果从注册表删除有关组件的所有信息。 这些函数不会实际删除 component; 的文件安装程序会尝试如果新的使用率计数为 0。
