---
title: 如果计划启用变更数据捕获，则删除 cdc 架构 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- cdc schema
- change data capture
ms.assetid: 6a84aa25-0f31-4be3-b2dd-4f249b8254ae
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cc580a6032a19eb8248759669278f8730fc617cb
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66092952"
---
# <a name="remove-the-cdc-schema-if-you-plan-to-enable-change-data-capture"></a>如果计划启用变更数据捕获则删除 cdc 架构
  数据库已经包含一个 cdc 架构。 如果计划在升级后启用变更数据捕获，则必须先删除此 cdc 架构。 当对数据库启用变更数据捕获时，[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]将创建一个名为 cdc 的新架构。  
  
  
