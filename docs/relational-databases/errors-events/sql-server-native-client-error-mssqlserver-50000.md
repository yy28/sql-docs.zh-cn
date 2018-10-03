---
title: MSSQLSERVER_50000 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: supportability
ms.topic: reference
helpviewer_keywords:
- 50000 [SQL Server Native Client setup error]
ms.assetid: 5426d87a-d5d9-4984-b211-b07d69e834a2
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: aaf143c4a02c0faca0d61104dd8cbaf9eaf6e0e0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47825775"
---
# <a name="sql-server-native-client-error-mssqlserver50000"></a>SQL Server 本机客户端错误 MSSQLSERVER_50000
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|产品版本|11.0|  
|事件 ID|50000|  
|事件源|SETUP|  
|组件|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client|  
|符号名称||  
|消息正文|尝试从文件“%.*ls”中读取内容时出现网络错误。|  
  
## <a name="explanation"></a>解释  
 尝试在满足以下条件的计算机上安装（或更新） [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client：已安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client，并且现有安装是来自从 sqlncli.msi 重命名的 MSI 文件。  
  
## <a name="user-action"></a>用户操作  
 若要解决此错误，请卸载 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 的现有版本。 若要防止此错误，请不要从未命名为 sqlncli.msi 的 MSI 文件安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client。  
  
## <a name="internal-only"></a>仅内部  
  
