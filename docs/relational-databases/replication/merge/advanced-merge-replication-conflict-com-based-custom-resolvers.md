---
title: 基于 COM 的自定义冲突解决程序 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- COM-based resolvers [SQL Server replication]
- custom resolvers [SQL Server replication]
ms.assetid: 94195797-ad7a-4962-a8e3-b259cd13aa38
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e6555af4448af4e9e1e4e14f2e4e23f1407f0681
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2019
ms.locfileid: "54135987"
---
# <a name="advanced-merge-replication-conflict---com-based-custom-resolvers"></a>高级合并复制冲突 - 基于 COM 的自定义解决程序
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  与默认解决机制相比，自定义冲突解决程序提供了更大的灵活性，可以实现使用复制数据的应用程序所需的业务逻辑。 基于 COM 的自定义冲突解决程序是一个动态链接库 (DLL)，它实现了 **ICustomResolver** COM 接口、方法、属性以及其他专为解决冲突设计的支持接口和类型定义。  
  
> [!NOTE]  
>  如果可能，建议使用业务逻辑处理程序而非基于 COM 的自定义冲突解决程序。 有关业务逻辑处理程序的详细信息，请参阅[合并同步期间执行业务逻辑](../../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md)。  
  
 若要创建自定义的 COM 冲突解决程序，可以使用 replrec.dll 中提供的类型库；默认情况下，此类型库安装在 [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]COM 下。  
  
 编写自定义的 COM 冲突解决程序之前，需要决定以下事项：  
  
-   要解决的行更改类型（例如更新、插入和删除）以及是否在上载和/或下载合并更改过程中调用冲突解决程序。 可以指定一种类型的更改、所有更改或任何组合。 默认的合并冲突解决程序处理自定义冲突解决程序未处理的所有冲突。  
  
-   是否在解决冲突时使用列跟踪。 当列级跟踪处于开启状态时，只有那些存在冲突的行中的数据才标志为冲突，否则合并这些数据。 但是，解决冲突的方式与行级跟踪相同：优先级入选方覆盖整行数据（但数据可以是来自发布服务器、订阅服务器的混合值，也可以是既不来自发布服务器也不来自订阅服务器的某些更改值）。 有关详细信息，请参阅 [检测并解决合并复制冲突](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)。  
  
 若要实现基于 COM 的自定义冲突解决程序，请参阅 [为合并项目实现自定义冲突解决程序](../../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md)。  
  
 自定义冲突解决程序是针对项目而不是整个发布指定的。 同一个冲突解决程序可用于多个项目，但自定义冲突解决程序中的逻辑通常针对特定的表。 如果在创建冲突解决程序后修改了项目中使用的表（例如，为冲突解决中所用列名重命名），那么自定义冲突解决程序就可能需要修改并重新编译。  
  
 若要指定自定义冲突解决程序，请参阅 [指定合并项目冲突解决程序](../../../relational-databases/replication/publish/specify-a-merge-article-resolver.md)。  
  
## <a name="see-also"></a>另请参阅  
 [高级合并复制冲突检测和解决](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Microsoft COM-Based Resolvers](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-resolvers.md)  
  
  
