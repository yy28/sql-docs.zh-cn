---
title: 安装程序 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b89cae70db65bd2aa54b8e9789a5c2b35696923e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296147"
---
# <a name="setup-program"></a>安装程序
> **注：** 从 Windows XP 和 Windows 服务器 2003 开始 **，ODBC 包含在 Windows 操作系统中**。 您只应在早期版本的 Windows 上显式安装 ODBC。  
  
 用户运行安装程序以启动安装过程。 安装程序由应用程序或驱动程序开发人员编写。 除了安装 ODBC 组件外，还可以安装其他软件。 例如，应用程序开发人员可能使用相同的安装程序来安装 ODBC 组件并安装其应用程序。  
  
 开发人员可以使用 Microsoft ® Windows ® SDK 设置实用程序或来自其他供应商的设置软件，从头开始编写安装程序。 这使得这些开发人员能够完全控制安装程序的外观。 可以编写安装程序来安装其他软件，如 ODBC 应用程序。 有关 Windows SDK 设置实用程序的详细信息，请参阅 Windows SDK 文档。  
  
 安装程序实际完成安装量取决于安装程序 DLL 中调用的功能。 安装程序 DLL 包含安装单个 ODBC 组件的功能。 安装程序只需在安装程序 DLL 中调用**SQLInstallDriverManager、SQLInstallDriverEx**或**SQLInstallTranslatorEx，** 即可检索要在其中安装组件的目录的路径，并将有关组件的信息添加到注册表中。 **SQLInstallDriverEx** 这些函数实际上不复制文件;因此，这些函数不会复制文件。安装程序使用这些函数参数中的信息来这样做。  
  
 安装程序 DLL 还包含删除 ODBC 组件的功能。 安装程序在安装程序 DLL 中调用**SQLRemoveDriverManager、SQLRemoveDriver**或**SQLRemove 转换器**，以在注册表中减少组件的使用计数，如果组件的新使用计数降至 0，则从注册表中删除有关该组件的所有信息。 **SQLRemoveDriver** 这些函数实际上不会删除组件的文件，而是删除组件的文件。如果新的使用计数下降到 0，安装程序将执行此项。
