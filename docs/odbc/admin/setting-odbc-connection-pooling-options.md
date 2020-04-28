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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1d8e66c506518b77320347ce9120254aa1cae287
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307190"
---
# <a name="setting-odbc-connection-pooling-options"></a>设置 ODBC 连接池选项
使用连接池，应用程序可以使用连接池的连接，无需在每次使用时重新建立连接。 您可以使用 " **ODBC 数据源管理器**" 对话框的 "**连接池**" 选项卡来启用和禁用性能监视。 双击驱动程序名称以设置连接超时期限。  
  
 在驱动程序级别，通过 CPTimeout 注册表值启用连接池。 此选择性每个驱动程序启用允许系统管理员只为可支持它的驱动程序启用连接池。 这是通过在驱动程序的安装程序中设置 CPTimeout 的默认值来实现的。 双击驱动程序名称以设置连接超时期限。  
  
 有关连接池的详细信息，请参阅[ODBC 连接池](../../odbc/reference/develop-app/driver-manager-connection-pooling.md)。  
  
## <a name="performance-monitoring"></a>性能监视  
 性能监视通过记录各种统计信息来跟踪连接性能。 开发人员可以自定义这些统计信息，以包含如下所示的项目：  
  
|计数器|定义|  
|-------------|----------------|  
|ODBC Hard Connection 计数器 per Second|每秒与服务器建立的实际连接数。 当你的环境第一次出现繁重负载时，此计数器的速度会非常快。 几秒钟后，它将降到零。 这是连接池正常运行时的正常情况。 建立与服务器的连接后，将使用这些连接并将其放入池中以供重复使用。|  
|ODBC Hard Disconnect 计数器 per Second|每秒发送到服务器的硬断开连接数。 这些是连接池正在释放的服务器的实际连接。 当你停止系统上的所有客户端并使连接超时时，此值将从零开始增加。|  
|ODBC 软连接计数器/秒|每秒池满足的连接数-换言之，是指从池中传递给用户的连接数。 此计数器指示池是否正常工作。 根据服务器上的负载，这种情况并不常见，因为每秒显示40-60 软连接。|  
|ODBC 软断开计数器/秒|应用程序发出的每秒断开连接数。 当应用程序释放或断开连接时，该连接将返回到池中。|  
|ODBC 当前活动连接计数器|池中当前正在使用的连接数。|  
|ODBC 当前可用连接计数器|池中可用的当前空闲连接数。 这些是可供使用的实时连接。|  
|当前处于活动状态的池|当前处于活动状态的池的数目。 此计数器是在 Windows 8 中添加的，用于管理连接池中的连接的驱动程序。 有关详细信息，请参阅[识别驱动程序的连接池](../../odbc/reference/develop-app/driver-aware-connection-pooling.md)。|  
|已创建池|处于活动状态的池数，包括活动的和已删除的池。 此计数器是在 Windows 8 中添加的，用于管理连接池中的连接的驱动程序。 有关详细信息，请参阅[识别驱动程序的连接池](../../odbc/reference/develop-app/driver-aware-connection-pooling.md)。|  
  
 您必须指定您自己的监视参数。 此版本的 ODBC 附带了用于性能监视的示例。
