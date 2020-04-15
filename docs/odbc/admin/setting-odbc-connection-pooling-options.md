---
title: 设置 ODBC 连接池选项 |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307190"
---
# <a name="setting-odbc-connection-pooling-options"></a>设置 ODBC 连接池选项
连接池使应用程序能够使用连接池中的连接，而不需要为每个使用重新建立连接池。 您可以使用**ODBC 数据源管理员**对话框的连接**池**选项卡来启用和禁用性能监视。 双击驱动程序名称以设置连接超时时间。  
  
 在驱动程序级别，连接池由 CPTimeout 注册表值启用。 这种选择性的每个驱动程序启用允许系统管理员仅为支持它的驱动程序启用连接池。 通过在驱动程序设置程序期间设置 CPTimeout 的默认值来实现。 双击驱动程序名称以设置连接超时时间。  
  
 有关连接池的详细信息，请参阅[ODBC 连接池](../../odbc/reference/develop-app/driver-manager-connection-pooling.md)。  
  
## <a name="performance-monitoring"></a>性能监视  
 性能监控通过记录各种统计信息来跟踪连接性能。 开发人员可以自定义这些统计信息，以包括以下项：  
  
|计数器|定义|  
|-------------|----------------|  
|ODBC 硬连接计数器每秒|每秒对服务器进行的实际连接数。 第一次你的环境携带重负荷时，这个计数器会很快上升。 几秒钟后，它将下降到零。 这是连接池工作时的正常情况。 建立与服务器的连接后，将使用这些连接并将其放置在池中以供重用。|  
|ODBC 每秒硬断开计数器|每秒颁发给服务器的硬断开连接数。 这些是连接池释放的服务器的实际连接。 当您停止系统上的所有客户端并且连接开始超时时，此值将从零增加。|  
|ODBC 每秒软连接计数器|池每秒满足的连接数，换句话说，从该池交给用户的连接。 此计数器指示池是否工作。 根据服务器上的负载，每秒显示 40-60 个软连接的情况并不少见。|  
|ODBC 每秒软断开计数器|应用程序每秒发出的断开连接数。 当应用程序释放或断开连接时，连接将放回池中。|  
|ODBC 当前活动连接计数器|池中当前正在使用的连接数。|  
|ODBC 电流自由连接计数器|池中可用的当前可用连接数。 这些是可用的实时连接。|  
|池当前处于活动状态|当前处于活动状态的池数。 此计数器在 Windows 8 中添加，用于管理连接池中连接的驱动程序。 有关详细信息，请参阅[驱动程序感知连接池](../../odbc/reference/develop-app/driver-aware-connection-pooling.md)。|  
|已创建池|活动池数，包括活动池和已删除池。 此计数器在 Windows 8 中添加，用于管理连接池中连接的驱动程序。 有关详细信息，请参阅[驱动程序感知连接池](../../odbc/reference/develop-app/driver-aware-connection-pooling.md)。|  
  
 您必须指定自己的监视参数。 此版本的 ODBC 中已包含用于性能监控的样本。
