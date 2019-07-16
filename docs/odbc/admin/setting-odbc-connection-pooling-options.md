---
title: 设置 ODBC 连接池选项 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection pooling [ODBC]
- ODBC data source administrator [ODBC], connection pooling options
- ODBC data source administrator [ODBC], performance monitoring
ms.assetid: 037e2f78-f204-40f4-b4ab-d9cdf562012b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 43d4fe1ab363326269daf40375e126b930d2548b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67901643"
---
# <a name="setting-odbc-connection-pooling-options"></a>设置 ODBC 连接池选项
连接池使应用程序能够从无需每次使用重新建立连接的连接池使用连接。 可以使用**连接池**选项卡**ODBC 数据源管理器**对话框来启用和禁用性能监视。 双击要设置连接超时期限的驱动程序名称。  
  
 在驱动程序级别启用连接池是由 CPTimeout 注册表值。 此选择性的每个驱动程序启用允许系统管理员联系以启用连接池只是驱动程序可支持它。 通过在驱动程序的安装程序过程中设置 CPTimeout 的默认值。 双击要设置连接超时期限的驱动程序名称。  
  
 有关连接池的详细信息，请参阅[ODBC 连接池](../../odbc/reference/develop-app/driver-manager-connection-pooling.md)。  
  
## <a name="performance-monitoring"></a>性能监视  
 性能监视通过记录各种统计信息来跟踪连接性能。 这些统计信息可以由开发人员，如下所示的项包含自定义：  
  
|计数器|定义|  
|-------------|----------------|  
|每秒的 ODBC 硬连接计数器|每秒实际与服务器建立的连接数。 第一次你的环境携带负载过重时，此计数器将会增加速度非常快。 几秒钟后，它将降为零。 使用连接池时，这是正常情况。 如果已建立到服务器的连接，它们将使用，放入以供重复使用池。|  
|ODBC 硬断开连接每秒的计数器|每秒发送到服务器断开连接的数量硬。 这些是实际连接到服务器所发布的连接池。 此值将增加从零开始时在系统上停止所有客户端，连接将开始超时。|  
|每秒的 ODBC 软连接计数器|第二个中其他单词，从连接池中的每池满意的连接数已传递给用户。 此计数器指示池是否工作。 具体取决于你的服务器上的负载，不常见的此项以显示每秒 40-60 软连接数。|  
|每秒的 ODBC 软断开连接计数器|每秒颁发的应用程序断开连接的数量。 当应用程序释放或断开连接时，连接位于在池中。|  
|ODBC 当前活动连接计数器|当前正在使用池中的连接数。|  
|ODBC 当前可用的连接计数器|当前的池中可用的可用连接数。 这些是可供使用的实时连接。|  
|池当前处于活动状态|池当前处于活动状态的数量。 为管理连接池中连接的驱动程序在 Windows 8 中，添加了此计数器。 有关详细信息，请参阅[识别驱动程序的连接池](../../odbc/reference/develop-app/driver-aware-connection-pooling.md)。|  
|创建的池|池处于活动状态，包括活动和已删除池的数量。 为管理连接池中连接的驱动程序在 Windows 8 中，添加了此计数器。 有关详细信息，请参阅[识别驱动程序的连接池](../../odbc/reference/develop-app/driver-aware-connection-pooling.md)。|  
  
 必须指定您自己的监视参数。 与此版本的 ODBC 包含了用于性能监视的示例。
