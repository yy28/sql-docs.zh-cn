---
title: 群集网络配置 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- cluster network selection, Setup
- cluster network selection
ms.assetid: 579482ef-a023-45b2-9176-b4a4188adf9d
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 04b0d412cd577fb0869f2188d99c1ea6a5646d2b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85037173"
---
# <a name="cluster-network-configuration"></a>群集网络配置
  使用 **“群集网络选择”** 页可为故障转移群集实例指定网络资源。  
  
## <a name="options"></a>选项  
 ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集网络名称**-这是用于在网络上标识故障转移群集实例的名称。  
  
 **网络设置** - 指定故障转移群集实例的 IP 类型和 IP 地址。  
  
 在“添加节点”和“删除节点”操作期间， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 显示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集的现有 IP 地址的只读列表。  
  
-   集成安装：  
  
    -   如果您要添加一个节点，此节点支持由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集的现有节点支持的同一组网络子网，则不能添加其他 IP 地址。 依赖关系设置保持不变。  
  
    -   如果您要添加一个节点，此节点支持由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集上的现有节点支持的子网的一个子集，则不能添加其他 IP 地址资源。 IP 地址资源依赖关系设置为 OR，以反映指定的所有 IP 地址并非在所有群集节点上都有效。  
  
    -   如果您要添加一个节点，此节点除了支持由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集中的现有节点已经支持的子网之外，还支持其他子网，则您可以选择添加新的有效 IP 地址。 如果指定了新的 IP 地址，则 IP 地址资源依赖关系设置为 OR，以反映指定的所有 IP 地址并非在所有群集节点上都有效。  
  
    -   如果您要添加一个节点，此节点支持其他网络子网，但不支持由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集中的现有节点支持的子网，则您需要添加其他 IP 地址。 IP 地址资源依赖关系设置为 OR，以反映指定的所有 IP 地址并非在所有群集节点上都有效。  
  
-   高级安装：在安装过程的“完成”步骤中，为故障转移群集实例的所有节点和子网指定 IP 地址。 您可以为一个多子网故障转移群集指定多个 IP 地址，但每个子网只支持一个 IP 地址。 准备好的每个节点应至少是一个 IP 地址的所有者。 如果您在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 故障转移群集中有多个子网，系统将提示您将 IP 地址资源依赖关系设置为 OR。删除节点：  
  
    -   如果在所有剩余节点上都支持剩下的 IP 地址，系统会提示您将 IP 地址资源依赖关系设置为 AND。  
  
    -   如果并非在所有剩余节点上都支持剩下的 IP 地址，则 IP 地址资源依赖关系保留为 OR。  
  
  
