---
title: 使用数据源 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 52015cb202f46c50c16dcab408bed7761f0925db
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67951806"
---
# <a name="using-data-sources"></a>使用数据源
数据源通常由最终用户或技术人员使用称为*ODBC 管理员*的程序创建。 ODBC 管理器提示用户提供要使用的驱动程序，然后调用该驱动程序。 驱动程序将显示一个对话框，该对话框请求连接到数据源所需的信息。 用户输入信息后，该驱动程序会将其存储在系统中。  
  
 稍后，应用程序将调用驱动程序管理器，并向其传递计算机数据源的名称或包含文件数据源的文件的路径。 在传递计算机数据源名称时，驱动程序管理器会搜索系统以查找数据源使用的驱动程序。 然后，它会加载驱动程序并将数据源名称传递给它。 驱动程序使用数据源名称来查找连接到数据源所需的信息。 最后，它连接到数据源，通常会提示用户输入通常不会存储的用户 ID 和密码。  
  
 传递文件数据源时，驱动程序管理器将打开该文件并加载指定的驱动程序。 如果文件还包含一个连接字符串，则会将其传递给驱动程序。 使用连接字符串中的信息，驱动程序连接到数据源。 如果未传递连接字符串，驱动程序通常会提示用户提供必要的信息。
