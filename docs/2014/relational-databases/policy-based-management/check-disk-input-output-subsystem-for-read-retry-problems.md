---
title: 检查磁盘输入输出子系统是否存在读取重试问题 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: cedf4097-5b73-4964-9935-74a101847019
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 19809b1554e435600eb4eeae424bed17dc27bdbb
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85068988"
---
# <a name="check-disk-input-output-subsystem-for-read-retry-problems"></a>检查磁盘 I/O 子系统是否存在读取重试问题
  此规则检查事件日志中是否存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误消息 825。 此错误消息指示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 无法在第一次尝试时从磁盘读取数据。 此消息指示磁盘 I/O 子系统存在严重问题。 此消息当前不指示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 问题。 但是，如果不解决此磁盘问题，可能导致数据丢失或数据库损坏。  
  
## <a name="best-practices-recommendations"></a>最佳做法建议  
 下列操作可帮助您发现并解决基本的硬件问题：  
  
-   查阅错误日志和此消息中的变量文本以获得说明问题的线索。  
  
-   检查磁盘系统。 此问题可能与磁盘、磁盘控制器、阵列卡或磁盘驱动程序有关。  
  
-   与磁盘制造商联系以获得用于检查磁盘系统状态的最新实用工具。  
  
-   与磁盘制造商联系以获得最新的驱动程序。  
  
## <a name="for-more-information"></a>有关详细信息  
 [MSSQLSERVER_825](../errors-events/mssqlserver-825-database-engine-error.md)  
  
 [SQL Server I/O Basics, Chapter 2（SQL Server I/O 基础知识第 2 章）](/previous-versions/sql/sql-server-2005/administrator/cc917726(v=technet.10))  
  
  
