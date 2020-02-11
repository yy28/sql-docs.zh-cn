---
title: 管理计划 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- administration program [ODBC]
- ODBC administrator [ODBC]
ms.assetid: a6c8248a-7a01-42e7-aaed-99dc94d50028
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9cb78dae32bb17598ee0e86c26e621be1b6362c6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68068555"
---
# <a name="administration-program"></a>管理程序
> [!NOTE]  
>  从 Windows XP 和 Windows Server 2003 开始，ODBC 包含在 Windows 操作系统中。 只应在早期版本的 Windows 上显式安装 ODBC。  
  
 Windows SDK/MDAC SDK 中包含管理程序（ODBC 管理员）。 此程序可由 SDK 用户重新分发。 此外，开发人员还可以编写自己的管理程序。 通常，仅当开发人员想要保留对数据源配置的完全控制，或者如果直接从充当管理程序的应用程序配置数据源时，开发人员才会编写自己的管理程序。 例如，电子表格程序可能允许用户在运行时添加和使用数据源。  
  
 管理程序首先加载安装程序 DLL。 然后，它调用安装程序 DLL 中的函数来执行以下任务：  
  
-   **以交互方式添加、修改或删除数据源。** 管理程序可以调用**SQLManageDataSources**、 **SQLCreateDataSource**或**SQLConfigDataSource**。  
  
     **SQLManageDataSources**显示一个对话框，用户可以使用该对话框添加、修改或删除数据源并指定跟踪选项;当直接从控制面板调用安装程序 DLL 时，将调用此函数。 **SQLCreateDataSource**显示一个对话框，用户只能在其中添加数据源。 **SQLConfigDataSource**将调用直接传递给驱动程序安装程序 DLL。  
  
     在所有情况下，安装程序 DLL 都调用驱动程序安装程序 DLL 中的**ConfigDSN** ，以实际添加、修改或删除数据源。 驱动程序安装程序 DLL 可能会提示用户输入其他信息。  
  
-   **以无提示方式添加、修改或删除数据源。** 管理程序在安装程序 DLL 中调用**SQLConfigDataSource** ，并向其传递一个空窗口句柄、要添加、修改或删除的数据源的名称和注册表值的列表。 安装程序 DLL 调用驱动程序安装程序 DLL 中的**ConfigDSN** ，以实际添加、修改或删除数据源。  
  
-   **添加、修改或删除默认数据源。** 默认数据源与任何其他数据源相同，不同之处在于其名称为默认值。 添加、修改或删除了与任何其他数据源相同的方式。
