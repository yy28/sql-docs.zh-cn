---
title: "新对等方的初始化（对等复制）| Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.p2pwizard.init.f1
ms.assetid: 050c00e1-78bd-4d9c-affe-40e22feb4d94
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b365d21c3754b9bb175dd8c47baedbc8318ef391
ms.lasthandoff: 04/11/2017

---
# <a name="new-peer-initialization-peer-to-peer-replication"></a>新对等方的初始化（对等复制）
  可以使用 **“新对等方初始化”** 页指定如何初始化对等数据库。 （在完成此向导之前，必须初始化对等方。）可以采用手动方式来初始化对等方，或使用事务复制提供的 **initialize with backup** 功能来初始化对等方。 （对等事务复制不支持使用快照初始化对等方。）如果必须使用其他方法来初始化其他对等方，则必须分别运行几次向导来添加对等方。  
  
## <a name="options"></a>选项  
 **指定如何初始化新的对等数据库**  
 所有已发布对象的架构和数据必须存在于每个对等方。 选择以下选项之一：  
  
-   如果已经手动为已发布的对象创建了架构，或者已经还原了备份，并且在此备份后第一个发布数据库的数据未更改，则可以选择第一个选项。 如果手动创建了架构，则必须确保每个对等方存在所有所需的数据。 此选项对应于订阅属性 **sync_type** 的 **replication support only**值。  
  
-   如果您已经还原了备份，并且在此备份后第一个发布数据库的数据发生了更改，则可以选择第二个选项。 复制必须立即传递备份中不包括的第一个发布数据库的更改。 此选项对应于订阅属性 **sync_type** 的 **initialize with backup**值。  
  
     为对等复制启用发布时，将设置 **allow_initialize_from_backup** 发布属性。 复制立即开始跟踪在第一个发布数据库中所做的更改。 因此，如果选择了 **initialize with backup** 选项，则可以将这些更改传递给一个或多个对等方上的已还原数据库。 单击 **“浏览”** 按钮以找到所使用的备份，然后复制将从该备份中读取日志序列号 (LSN)。 具有较高 LSN 的第一个发布数据库中的所有更改都将传递到每个对等方。  
  
     如果是创建或添加到包含 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]的拓扑中，则此选项可能不可用。 下表显示了当将节点添加到现有拓扑中时此选项是否可用。  
  
    |新节点|第一个节点|其他节点|选项|  
    |--------------|----------------|----------------------|------------|  
    |[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|禁用|  
    |[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|无|禁用|  
    |[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|禁用|  
    |[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|无|已启用|  
    |[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|无|已启用|  
    |[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|已启用|  
    |[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|无|已启用|  
  
## <a name="see-also"></a>另请参阅  
 [管理对等拓扑（复制 Transact-SQL 编程）](../../relational-databases/replication/administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [对等事务复制](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  
