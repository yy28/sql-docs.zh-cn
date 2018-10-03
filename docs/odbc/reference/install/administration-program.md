---
title: 管理程序 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 740a09d9a6bceb9d3f290faa71444df0d1e7c6c7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47792315"
---
# <a name="administration-program"></a>管理程序
> [!NOTE]  
>  从 Windows XP 和 Windows Server 2003 开始，ODBC 包括在 Windows 操作系统中。 在早期版本的 Windows 上，应仅显式安装 ODBC。  
  
 管理程序，ODBC 管理器，将包含在 Windows SDK/MDAC SDK。 此程序并重新发布的可由用户的 sdk。 此外，开发人员可以编写自己的管理程序。 通常情况下，开发人员编写自己的管理程序，仅当他们想要保留对数据源配置完全控制，或如果它们要配置直接从充当管理程序的应用程序的数据源。 例如，电子表格程序可能允许用户添加，然后在运行时使用数据源。  
  
 管理程序第一次加载安装程序 DLL。 然后，它会在安装程序中执行以下任务的 DLL 调用函数：  
  
-   **添加、 修改或删除数据源以交互方式。** 管理程序可以调用**SQLManageDataSources**， **SQLCreateDataSource**，或**SQLConfigDataSource**。  
  
     **SQLManageDataSources**显示一个对话框，可使用该用户可以添加、 修改或删除数据源和指定跟踪选项; 直接从控制面板中调用安装程序 DLL 时调用此函数。 **SQLCreateDataSource**显示一个对话框，使用该用户可以仅添加数据源。 **SQLConfigDataSource**传递直接对驱动程序安装程序 DLL 的调用。  
  
     在所有情况下，安装程序 DLL 调用**ConfigDSN**中的驱动程序安装 DLL 实际上添加、 修改或删除数据源。 驱动程序安装程序 DLL 可能会提示用户提供其他信息。  
  
-   **添加、 修改或以无提示方式删除数据源。** 在管理程序调用**SQLConfigDataSource**中的安装程序 DLL 和传递它 null 窗口处理，要添加、 修改或删除的数据源的名称和注册表值的列表。 安装程序 DLL 调用**ConfigDSN**中的驱动程序安装 DLL 实际上添加、 修改或删除数据源。  
  
-   **添加、 修改或删除默认数据源。** 默认数据源具有与任何其他数据源相同，只不过其名称是默认值。 它是添加、 修改或删除同一方式与任何其他数据源。
