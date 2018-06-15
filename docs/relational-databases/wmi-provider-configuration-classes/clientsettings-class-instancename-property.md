---
title: InstanceName 属性 （ClientSettings 类） |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: wmi
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- InstanceName Property (ClientSettings Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- InstanceName property
ms.assetid: 58dacb4a-751a-491f-9adb-88ec6afc797c
caps.latest.revision: 27
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 44ae9620a8bff93acac1d0287d1d705a4762e5ef
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33006544"
---
# <a name="clientsettings-class---instancename-property"></a>ClientSettings 类-InstanceName 属性
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  获取 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 客户端实例的名称。  
  
## <a name="syntax"></a>语法  
  
```  
  
object.InstanceName [= value]  
```  
  
## <a name="parts"></a>组成部分  
 *对象*  
 A **ClientSettings**对象，表示对设置[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]客户端实例。  
  
## <a name="property-valuereturn-value"></a>属性值/返回值  
 一个指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 客户端实例的名称的字符串值。  
  
## <a name="remarks"></a>注释  
  
