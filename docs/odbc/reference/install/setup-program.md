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
ms.openlocfilehash: dc79bb5d12b53938e3e2ef1c531fd03b0002ed78
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68093834"
---
# <a name="setup-program"></a>安装程序
> **注意：** 从 Windows XP 和 Windows Server 2003 开始， **ODBC 包含在 windows 操作系统中**。 只应在早期版本的 Windows 上显式安装 ODBC。  
  
 用户运行安装程序以启动安装过程。 安装程序由应用程序或驱动程序开发人员编写。 除了安装 ODBC 组件以外，它还可以安装其他软件。 例如，应用程序开发人员可能会使用相同的安装程序来安装 ODBC 组件和安装应用程序。  
  
 开发人员可以使用 Microsoft® Windows® SDK 安装实用工具或从其他供应商处安装软件，从头开始编写安装程序。 这样，开发人员就可以完全控制安装程序的外观。 可以编写安装程序来安装其他软件，例如 ODBC 应用程序。 有关 Windows SDK 安装程序实用工具的详细信息，请参阅 Windows SDK 文档。  
  
 安装程序实际完成多少安装取决于它在安装程序 DLL 中调用的功能。 安装程序 DLL 包含用于安装单个 ODBC 组件的函数。 安装程序只需在安装程序 DLL 中调用**SQLInstallDriverManager**、 **SQLInstallDriverEx**或**SQLInstallTranslatorEx** ，即可检索要在其中安装组件的目录的路径，并将有关组件的信息添加到注册表中。 这些函数实际上不会复制文件;安装程序将使用这些函数的参数中的信息来执行此过程。  
  
 安装程序 DLL 还包含用于删除 ODBC 组件的函数。 安装程序会在安装程序 DLL 中调用**SQLRemoveDriverManager**、 **SQLRemoveDriver**或**SQLRemoveTranslator** ，以便在注册表中减少组件的使用计数，如果组件的新用量计数降到0，则从注册表中删除有关组件的所有信息。 这些函数实际上不会删除组件的文件;如果新的使用计数降到0，则安装程序将执行此过程。
