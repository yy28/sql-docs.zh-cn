---
title: 安装程序 |Microsoft Docs
ms.custom: ''
ms.date: 08/31/2016
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- installing ODBC components [ODBC], setup program
ms.assetid: 9cc5d75d-b293-41e5-927c-10f4af2e7af1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f64eda5ad640e50afd25db111de74141e41e652d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63280779"
---
# <a name="setup-program"></a>安装程序
> **注意**：从 Windows XP 和 Windows Server 2003 **ODBC 包含在 Windows 操作系统**。 在早期版本的 Windows 上，应仅显式安装 ODBC。  
  
 用户运行安装程序，开始安装过程。 安装程序是应用程序或驱动程序开发人员编写的。 除了安装 ODBC 组件，它可以安装其他软件。 例如，应用程序开发人员可能会使用相同的安装程序来安装 ODBC 组件并安装其应用程序。  
  
 开发人员可以从头开始编写安装程序，使用 Microsoft® Windows® SDK 安装实用程序或来自其他供应商的安装程序软件。 这样，这些开发人员对安装程序的外观和感觉的完全控制。 可以编写安装程序为安装其他软件，例如 ODBC 应用程序。 有关 Windows SDK 安装程序工具的详细信息，请参阅 Windows SDK 文档。  
  
 安装多少实际上完成的安装程序依赖于它函数中的安装程序 DLL 的调用。 安装程序 DLL 包含用于安装各个 ODBC 组件函数。 安装程序只需调用**SQLInstallDriverManager**， **SQLInstallDriverEx**，或**SQLInstallTranslatorEx**在安装程序 DLL，若要检索的路径目录中的组件是在安装并向注册表添加有关组件的信息。 这些函数不实际复制文件;安装程序会尝试使用这些函数的参数中的信息。  
  
 安装程序 DLL 还包含用于删除 ODBC 组件函数。 在安装程序调用**SQLRemoveDriverManager**， **SQLRemoveDriver**，或**SQLRemoveTranslator** DLL 以减少组件的使用情况中安装程序中的数注册表和组件的新使用情况计数降为 0，如果从注册表删除有关该组件的所有信息。 这些函数不实际删除 component; 的文件安装程序执行此操作如果新的使用情况计数降为 0。
