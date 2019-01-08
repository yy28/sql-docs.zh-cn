---
title: 如何管理 CDC 实例 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5d9e677f-b872-497d-9cde-472184a214ab
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 058010d0e32fb26cf4c12e720342af04bd784768
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52804779"
---
# <a name="how-to-manage-a-cdc-instance"></a>How to Manage a CDC Instance
  本过程介绍如何使用 CDC 设计器控制台在运行时管理 CDC 实例操作。  
  
### <a name="to-manage-cdc-instance-operations"></a>管理 CDC 实例操作  
  
1.  从 **“开始”** 菜单上，选择 **“CDC 设计器控制台”**。  
  
2.  在左侧的窗格中，展开 **“变更数据捕获”** ，然后展开包含您要查看的实例的服务。  
  
3.  选择要使用的实例的名称。  
  
4.  从 CDC 设计器控制台右侧的 **“操作”** 窗格中，单击要执行的操作。  
  
     您还可以在左侧窗格中右键单击实例的名称，然后选择要执行的操作。  
  
     您可以执行以下任务：  
  
    -   **启动**:若要开始捕获更改。  
  
    -   **停止**:若要停止捕获更改  
  
    -   **重置**:单击“重置”可将 CDC 实例重置为其初始（空）状态。 此选项在 CDC 实例停止后可用。 更改表中的所有更改以及 CDC 实例内部状态将被删除。 当 CDC 实例在以后启动时，变更捕获将从该时间点开始，并且仅包含在 CDC 实例启动后开始的事务。  
  
    -   **删除**:若要删除 CDC 实例。  
  
    -   **Oracle 日志记录脚本**:单击**Oracle 日志记录脚本**以显示 Oracle 日志记录脚本对话框中具有 Oracle 补充日志记录脚本。 有关可以在此对话框中执行的操作的信息，请参阅 [Oracle Supplemental Logging Script](oracle-supplemental-logging-script.md)。  
  
         **注意**：在您运行补充日志记录脚本时，“用于运行脚本的 Oracle 凭据”对话框将打开，您可以在其中提供有效的 Oracle 用户名和密码。 有关如何提供适当的 Oracle 凭据的信息，请参阅 [Oracle Credentials for Running Script](oracle-credentials-for-running-script.md)。  
  
    -   **CDC 实例部署**:若要为 CDC 实例生成部署脚本。 有关此对话框的信息，请参阅 [CDC Instance Deployment Script](cdc-instance-deployment-script.md)。  
  
     有关这些任务的详细信息，请参阅 [Manage a CDC Instance](manage-a-cdc-instance.md)。  
  
 您还可以选择 **“属性”** 来编辑 CDC 实例的配置属性。 有关编辑 CDC 实例属性的详细信息，请参阅 [Edit Instance Properties](edit-instance-properties.md)。  
  
  
