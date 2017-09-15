---
title: "管理程序 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- administration program [ODBC]
- ODBC administrator [ODBC]
ms.assetid: a6c8248a-7a01-42e7-aaed-99dc94d50028
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 476c4710a4265214235bdd7b80a330fad5b37f34
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="administration-program"></a>管理程序
> [!NOTE]  
>  从 Windows XP 和 Windows Server 2003 开始，在 Windows 操作系统中包含 ODBC。 在早期版本的 Windows 上，应仅显式安装 ODBC。  
  
 管理程序，ODBC 管理器中，将包含在 Windows SDK/MDAC SDK。 此程序，可以通过用户的 sdk 一起重新分发。 此外，开发人员可以编写自己的管理程序。 通常情况下，开发人员编写自己的管理程序，仅当他们想要保留完整控制数据源配置，或如果它们要配置直接从充当管理程序的应用程序的数据源。 例如，电子表格程序可能允许用户添加，然后在运行时使用数据源。  
  
 管理程序首次加载安装程序 DLL。 然后，它会在安装程序中执行以下任务的 DLL 调用函数：  
  
-   **添加、 修改或删除数据源以交互方式。** 管理程序可以调用**SQLManageDataSources**， **SQLCreateDataSource**，或**SQLConfigDataSource**。  
  
     **SQLManageDataSources**显示一个对话框，可与该用户可以添加、 修改或删除数据源和指定跟踪选项; 安装程序 DLL 调用直接从控制面板时调用此函数。 **SQLCreateDataSource**显示一个对话框，使用该用户可以仅添加数据源。 **SQLConfigDataSource**传递直接对驱动程序安装程序 DLL 的调用。  
  
     在所有情况下，安装程序 DLL 调用**ConfigDSN**在驱动程序设置实际添加的 DLL 中，修改或删除数据源。 驱动程序安装程序 DLL 可能会提示用户提供其他信息。  
  
-   **添加、 修改或以无提示方式删除数据源。** 管理程序调用**SQLConfigDataSource**中的安装程序 DLL 和传递它 null 窗口处理，要添加、 修改或删除的数据源的名称和注册表值的列表。 安装程序 DLL 调用**ConfigDSN**在驱动程序设置实际添加的 DLL 中，修改或删除数据源。  
  
-   **添加、 修改或删除默认数据源。** 默认数据源具有与任何其他数据源，相同，只不过其名称是默认值。 它是添加、 修改或删除与任何其他数据源相同的方式。
