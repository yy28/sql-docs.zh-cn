---
title: 使用数据源 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], about data sources
ms.assetid: d5550619-22b2-4b16-bd08-fbabb6554c40
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: df9b09e4c5519e0fff44902bd83b8e3d92a67ca8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286537"
---
# <a name="using-data-sources"></a>使用数据源
数据源通常由最终用户或技术人员创建，其程序称为*ODBC 管理员*。 ODBC 管理员提示用户使用驱动程序，然后调用该驱动程序。 驱动程序显示一个对话框，该对话框请求连接到数据源所需的信息。 用户输入信息后，驱动程序将其存储在系统上。  
  
 稍后，应用程序调用驱动程序管理器，并传递计算机数据源的名称或包含文件数据源的文件的路径。 传递计算机数据源名称时，驱动程序管理器将搜索系统以查找数据源使用的驱动程序。 然后加载驱动程序并将数据源名称传递给它。 驱动程序使用数据源名称查找连接到数据源所需的信息。 最后，它连接到数据源，通常提示用户输入用户 ID 和密码，这些 ID 和密码通常不存储。  
  
 传递文件数据源时，驱动程序管理器将打开该文件并加载指定的驱动程序。 如果文件还包含连接字符串，它将将其传递给驱动程序。 使用连接字符串中的信息，驱动程序连接到数据源。 如果未传递连接字符串，驱动程序通常会提示用户获得必要的信息。
