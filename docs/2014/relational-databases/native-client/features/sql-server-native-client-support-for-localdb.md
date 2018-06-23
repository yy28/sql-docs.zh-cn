---
title: 对 LocalDB 的 SQL Server 本机客户端支持 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 127569d1-a9f7-49bf-a561-c084986a8871
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 144fe940cd1be0c2338e4e874658738b8854583d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36123608"
---
# <a name="sql-server-native-client-support-for-localdb"></a>SQL Server Native Client 对 LocalDB 的支持
  从 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 开始，将提供 SQL Server 的称作 LocalDB 的轻型版本。 本主题介绍如何连接到 LocalDB 实例中的数据库。  
  
## <a name="remarks"></a>Remarks  
 有关 LocalDB 的详细信息，包括如何安装 LocalDB 和配置您的 LocalDB 实例，请参阅：  
  
-   [SQL Server Express LocalDB 参考](../../sql-server-express-localdb-reference.md)  
  
-   [SQL Server 2014 Express LocalDB](../../../database-engine/configure-windows/sql-server-2016-express-localdb.md)  
  
 总之，通过 LocalDB，您可以：  
  
-   使用 `sqllocaldb.exe i` 发现默认实例的名称。  
  
-   使用 `AttachDBFilename` 连接字符串关键字指定服务器应附加的数据库文件。 使用时`AttachDBFilename`，如果不指定与数据库的名称**数据库**连接字符串关键字，将从 LocalDB 实例中的应用程序关闭时删除数据库。  
  
-   在您的连接字符串中指定 LocalDB 实例：  
  
```  
SERVER=(localdb)\v11.0  
```  
  
 如果需要，您可以使用 sqllocaldb.exe 创建 LocalDB 实例。 还可以使用 sqlcmd.exe 添加和修改 LocalDB 实例中的数据库。 例如， `sqlcmd -S (localdb)\v11.0`。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server Native Client 功能](sql-server-native-client-features.md)  
  
  