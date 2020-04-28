---
title: SQLXML 未安装在 SQL Server |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
ms.assetid: 3dbb4f65-41de-48b8-ad62-47c9d7932de3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8902c5dae5dea31393f658b13cb5c8773291f975
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "79112231"
---
# <a name="sqlxml-is-not-installed-in-sql-server"></a>SQL Server 中未安装 SQLXML
  在 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 之前，SQLXML 4.0 随 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 一起发布，是所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本（[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 除外）默认安装的一部分。 从 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 开始，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中不再包括 SQLXML 的最新版本 (SQLXML 4.0 SP1)。 若要在 SQLXML 4.0 SP1 可用时安装它，请从[SQLXML SP1 的安装位置进行](https://www.microsoft.com/download/details.aspx?id=44272)下载。  
  
 当某个应用程序在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上运行并且需要使用 SQLXML 4.0 时，如果计算机上没有安装 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]，则必须下载 SQLXML 4.0 SP1 并安装它。  
  
## <a name="sqlxml-40-sp1-behavior-with-new-data-types-using-sqloledb-and-sql-server-native-client-ole-db-provider"></a>在使用 SQLOLEDB 和 SQL Server Native Client OLE DB 访问接口的新数据类型时 SQLXML 4.0 SP1 的行为  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 中引入了以下数据类型，使用 SQLXML 的开发人员可能需要使用这些数据类型：  
  
-   `Date`  
  
-   `Time`  
  
-   `DateTime2`  
  
-   `DateTimeOffset`  
  
 如果将 SQLXML 4.0 SP1 与 SQLOLEDB（来自 Windows 数据访问组件，以前为 Microsoft 数据访问组件）或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB（来自 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]）一起使用，这些新类型将作为字符串显示给开发人员。 如果将 SQLXML 4.0 SP1 与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB Provider 11.0 一起使用，SQLXML 4.0 SP1 会将这四种新数据类型作为内置标量类型来使用。 在下载 SQLXML 4.0 SP1 之前，将这些类型映射到非字符串类型可能会导致截断某些数据。 `DateTime2`例如，映射`xsd:date`到将导致数据截断到[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] `DateTime` 3.33 毫秒。  
  
## <a name="see-also"></a>另请参阅  
 [SQLXML 4.0 编程概念](sqlxml-4-0-programming-concepts.md)  
  
  
