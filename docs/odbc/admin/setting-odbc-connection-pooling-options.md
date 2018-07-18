---
title: 设置 ODBC 连接池选项 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- connection pooling [ODBC]
- ODBC data source administrator [ODBC], connection pooling options
- ODBC data source administrator [ODBC], performance monitoring
ms.assetid: 037e2f78-f204-40f4-b4ab-d9cdf562012b
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: af8e9931c4026d578f226ec5e119815312c36a7a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32901293"
---
# <a name="setting-odbc-connection-pooling-options"></a>设置 ODBC 连接池选项
应用程序，从无需为每种使用重新建立的连接池使用连接可以连接池。 你可以使用**连接池**选项卡**ODBC 数据源管理器**对话框中，若要启用和禁用性能监视。 双击要设置的连接超时期限的驱动程序名称。  
  
 在驱动程序级别中，连接池被通过 CPTimeout 注册表值。 此选择性的每个驱动程序启用后，系统管理员联系，以启用连接池只需的驱动程序可以支持它。 它可以通过在驱动程序的安装程序过程中设置 CPTimeout 的默认值。 双击要设置的连接超时期限的驱动程序名称。  
  
 有关连接池的详细信息，请参阅[ODBC 连接池](../../odbc/reference/develop-app/driver-manager-connection-pooling.md)。  
  
## <a name="performance-monitoring"></a>性能监视  
 性能监视通过记录各种统计信息来跟踪连接性能。 由开发人员要包含项，如下所示，可以自定义这些统计信息：  
  
|计数器|定义|  
|-------------|----------------|  
|每秒的 ODBC 硬连接计数器|每秒实际与服务器建立的连接数。 第一次你的环境会带来负载过大，此计数器将转到上速度非常快。 几秒钟后，它将删除为零。 这是正常情况下，使用连接池时。 在建立了到服务器的连接，它们将使用和以供重复使用池中放置。|  
|ODBC 硬断开连接每秒的计数器|每秒发送到服务器断开连接的硬盘数。 这些是每天都发布的连接池的实际连接到服务器。 在系统上停止所有客户端，连接超时将开始时，此值将增加从零。|  
|每秒的 ODBC 软连接计数器|每秒池满意的连接数-换而言之，已传递给用户从该池连接。 此计数器指示是否工作池。 具体取决于你的服务器上的负载，是很常见的此项以显示每秒 40 到 60 软连接。|  
|每秒的 ODBC 软断开连接计数器|每秒由应用程序颁发断开连接的数目。 当应用程序释放或断开连接时，连接位于在池中。|  
|ODBC 当前活动连接计数器|当前正在使用池中的连接数。|  
|ODBC 当前可用的连接计数器|当前的池中可用的可用连接数。 这些是可供使用的实时连接。|  
|池当前处于活动状态|当前处于活动状态的池数。 此计数器在 Windows 8 中，添加了驱动程序管理连接池中的连接。 有关详细信息，请参阅[识别驱动程序的连接池](../../odbc/reference/develop-app/driver-aware-connection-pooling.md)。|  
|创建的池|池处于活动状态，包括活动的和已删除的池数。 此计数器在 Windows 8 中，添加了驱动程序管理连接池中的连接。 有关详细信息，请参阅[识别驱动程序的连接池](../../odbc/reference/develop-app/driver-aware-connection-pooling.md)。|  
  
 你必须指定你自己监视参数。 与此版本的 ODBC 包含了用于性能监视的示例。
