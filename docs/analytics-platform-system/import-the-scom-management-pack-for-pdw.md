---
title: 导入 SCOM 管理包-分析平台系统 |Microsoft 文档
description: 请按照下列步骤导入 System Center Operations Manager (SCOM) 管理包分析平台系统 (AP)。 监视 SCOM 中的并行数据仓库所需的管理包。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: e60d87ae58b0804a0a7296f8b489df7441683c5b
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/19/2018
ms.locfileid: "31538587"
---
# <a name="import-the-scom-management-pack---analytics-platform-system"></a>导入 SCOM 管理包-分析平台系统
请按照下列步骤导入 System Center Operations Manager (SCOM) 管理包分析平台系统 (AP)。 监视 SCOM 中的并行数据仓库所需的管理包。 
  
## <a name="BeforeBegin"></a>开始之前  
**先决条件**  
  
System Center Operations Manager 2007 R2 必须已安装并且正在运行。  
  
必须安装的管理包。 请参阅[安装 SCOM 管理包&#40;Analytics Platform System&#41;](install-the-scom-management-packs.md)。  
  
## <a name="Step1"></a>步骤 1： 导入 SQL Server 设备的基本管理包  
  
1.  登录到计算机时使用该帐户是 Operations Manager 2007 管理组的 Operations Manager 管理员角色的成员。  
  
2.  在操作控制台中，单击**管理**。  
  
3.  右键单击**管理包**节点，，然后单击**导入管理包**。  
  
    ![单击导入管理包](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP.png "SCOM_IMP")  
  
4.  在管理包列表中，选择你想要导入，请单击管理包**选择**，然后单击**添加**。  
  
    ![管理包列表](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP2.png "SCOM_IMP2")  
  
5.  搜索**设备**，然后深化到 SQL 服务器设备基本，然后单击**添加**两个选项。  
  
    ![SQL Server 设备基](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP3.png "SCOM_IMP3")  
  
6.  后两个管理包已在所选底部窗格中，然后单击**确定**。  
  
    ![选择这两个管理包](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP4.png "SCOM_IMP4")  
  
7.  单击 **“安装”**。  
  
    ![单击安装](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP5.png "SCOM_IMP5")  
  
8.  完成后，单击**关闭**。  
  
    ![完成后，单击关闭](./media/import-the-scom-management-pack-for-pdw/SCOM_IMP6.png "SCOM_IMP6")  
  
## <a name="Step2"></a>为 Microsoft SQL Server 2008 R2 并行数据仓库设备导入监视包  
  
1.  右键单击**管理包**节点，，然后单击**导入管理包**。  
  
2.  选择**从磁盘中的添加**...  
  
    ![右键单击管理包](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW.png "SCOM_PDW")  
  
3.  转到你在哪里提取 SQL Server PDW 管理包的位置，然后选择"所选管理包导入"部分中的三个管理包。 可以通过选择第一个、 单击 shift 键，并选择最后一个来执行此操作。 一旦所有已选中它们，单击**打开**。  
  
    ![选择管理包](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW2.png "SCOM_PDW2")  
  
4.  单击 **“安装”**。  
  
    ![单击安装](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW3.png "SCOM_PDW3")  
  
5.  单击 **“关闭”**。  
  
    ![单击关闭](./media/import-the-scom-management-pack-for-pdw/SCOM_PDW4.png "SCOM_PDW4")  
  
## <a name="next-step"></a>下一步  
现在，导入管理包之后，继续执行下一步：[到监视器 Analytics Platform System 配置 SCOM &#40;Analytics Platform System&#41;](configure-scom-to-monitor-analytics-platform-system.md)。  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
