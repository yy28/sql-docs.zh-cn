---
title: 管理计划 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d8a2a8363371d6f6c3644c2b7b49aa77644d496e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306638"
---
# <a name="administration-program"></a>管理程序
> [!NOTE]  
>  从 Windows XP 和 Windows 服务器 2003 开始，ODBC 包含在 Windows 操作系统中。 您只应在早期版本的 Windows 上显式安装 ODBC。  
  
 Windows SDK/MDAC SDK 中包括一个管理程序（ODBC 管理员）。 此程序，并且可以由 SDK 的用户重新分发。 此外，开发人员可以编写自己的管理程序。 通常，开发人员只有在希望保留对数据源配置的完全控制时，或者直接从充当管理程序的应用程序配置数据源时，才编写自己的管理程序。 例如，电子表格程序可能允许用户在运行时添加和使用数据源。  
  
 管理程序首先加载安装程序 DLL。 然后，调用安装程序 DLL 中的函数以执行以下任务：  
  
-   **以交互方式添加、修改或删除数据源。** 管理程序可以调用**SQLManageDataSource、SQLCreate****数据源**或**SQLConfigDataSource**。  
  
     **SQLManageDataSources**显示一个对话框，用户可以用该对话框添加、修改或删除数据源并指定跟踪选项;当直接从控制面板调用安装程序 DLL 时，将调用此功能。 **SQLCreateDataSource**显示一个对话框，用户可以使用该对话框添加数据源。 **SQLConfigDataSource**将呼叫直接传递到驱动程序设置 DLL。  
  
     在所有情况下，安装程序 DLL 在驱动程序设置 DLL 中调用**ConfigDSN**以实际添加、修改或删除数据源。 驱动程序设置 DLL 可能会提示用户以获取其他信息。  
  
-   **静默添加、修改或删除数据源。** 管理程序在安装程序 DLL 中调用**SQLConfigDataSource，** 并传递一个空窗口句柄、要添加、修改或删除的数据源的名称以及注册表的值列表。 安装程序 DLL 在驱动程序设置 DLL 中调用**ConfigDSN**以实际添加、修改或删除数据源。  
  
-   **添加、修改或删除默认数据源。** 默认数据源与任何其他数据源相同，只不过其名称为"默认"。 它以与任何其他数据源相同的方式添加、修改或删除。
