---
title: SQL Server Native Client 对 LocalDB 的支持 |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 127569d1-a9f7-49bf-a561-c084986a8871
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 57fe6bd159be275e9a183c1598b5cde5a82a44dd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "73761296"
---
# <a name="sql-server-native-client-support-for-localdb"></a>SQL Server Native Client 对 LocalDB 的支持
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  从 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 开始，将提供 SQL Server 的称作 LocalDB 的轻型版本。 本主题介绍如何连接到 LocalDB 实例中的数据库。  
  
## <a name="remarks"></a>备注  
 有关 LocalDB 的详细信息，包括如何安装 LocalDB 和配置您的 LocalDB 实例，请参阅：  
  
-   [SQL Server Express LocalDB 参考](../../../relational-databases/sql-server-express-localdb-reference.md)  
  
-   [SQL Server 2016 Express LocalDB](../../../database-engine/configure-windows/sql-server-2016-express-localdb.md)  
  
 总之，通过 LocalDB，您可以：  
  
-   使用**sqllocaldb**来发现默认实例的名称。  
  
-   使用 AttachDBFilename 连接字符串关键字指定服务器应附加的数据库文件****。 使用 AttachDBFilename 时，如果没有使用 Database 连接字符串关键字指定数据库的名称，则在应用程序关闭时，该数据库将从 LocalDB 实例中删除********。  
  
-   在您的连接字符串中指定 LocalDB 实例：  
  
```  
SERVER=(localdb)\v11.0  
```  
  
 如果需要，您可以使用 sqllocaldb.exe 创建 LocalDB 实例。 还可以使用 sqlcmd.exe 添加和修改 LocalDB 实例中的数据库。 例如， **sqlcmd-S （localdb） \v11.0**。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Native Client 功能](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
