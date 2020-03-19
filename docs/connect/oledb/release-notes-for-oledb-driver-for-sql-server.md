---
title: 发行说明 (OLE DB Driver for SQL Server)
ms.date: 02/27/2020
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
ms.reviewer: genemi
author: mateusz-kmiecik
ms.author: v-makmie
ms.openlocfilehash: c0a9e1726958a1eda7cf71817479f7c37dcfe854
ms.sourcegitcommit: 4bba3c8e3360bcbe269819d61f8898d0ad52c6e3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/11/2020
ms.locfileid: "79090529"
---
# <a name="release-notes-for-the-microsoft-ole-db-driver-for-sql-server"></a>适用于 SQL Server 的 Microsoft OLE DB 驱动程序发行说明

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

本页讨论添加到适用于 SQL Server 的 Microsoft OLE DB 驱动程序的每个版本中的内容。

<!--
USE THE TABLE FORMAT!
Hello, from now on, please use the table-based format standard for all new Release Notes content.
See section "## 18.2.1" for a live example in this article.
Thank you. For questions, contact GeneMi. (2019/03/16)
-->

## <a name="1830"></a>18.3.0

![下载](../../ssms/media/download-icon.png)[下载 x64 安装程序](https://go.microsoft.com/fwlink/?linkid=2117515)  
![下载](../../ssms/media/download-icon.png)[下载 x86 安装程序](https://go.microsoft.com/fwlink/?linkid=2117517)  

发布日期：2019 年 10 月

如果想要安装的语言版本不包含在检测到的语言中，可以使用以下直接链接。  
对于 x64 驱动程序：[中文（简体）](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x804) | [中文（繁体）](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x404) | [英语（美国）](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x409) | [法语](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x40c) | [德语](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x407) | [意大利语](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x410) | [日语](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x411) | [朝鲜语](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x412) | [葡萄牙语（巴西）](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x416) | [俄语](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x419) | [西班牙语](https://go.microsoft.com/fwlink/?linkid=2117515&clcid=0x40a)  
对于 x86 驱动程序：[中文（简体）](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x804) | [中文（繁体）](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x404) | [英语（美国）](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x409) | [法语](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x40c) | [德语](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x407) | [意大利语](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x410) | [日语](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x411) | [朝鲜语](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x412) | [葡萄牙语（巴西）](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x416) | [俄语](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x419) | [西班牙语](https://go.microsoft.com/fwlink/?linkid=2117517&clcid=0x40a)  

### <a name="features-added"></a>新增功能

| 新增功能 | 详细信息 |
| :------------ | :------ |
| Azure Active Directory 身份验证支持（`ActiveDirectoryInteractive`、`ActiveDirectoryMSI`）。 | [使用 Azure Active Directory](features/using-azure-active-directory.md)。 |
| 在安装程序中添加 Azure Active Directory 身份验证库 (adal.dll) | 现已包含在基础驱动程序安装中，OLE DB 安装程序将升级适用于 SQL Server 的 Microsoft Active Directory 身份验证库的现有安装，同时从 Windows 的已安装应用程序列表中将其删除。 |
| &nbsp; | &nbsp; |

### <a name="bugs-fixed"></a>已修复 bug

| 已修复 bug | 详细信息 |
| :-------- | :------ |
| 修复了 [IIndexDefinition::DropIndex](https://go.microsoft.com/fwlink/?linkid=2106448) 中的删除索引逻辑。 | 当索引所有者的架构 ID 和用户 ID 不相等时，旧版 OLE DB 驱动程序无法删除主键索引。 |
| &nbsp; | &nbsp; |

## <a name="previous-releases"></a>以前的版本

通过单击以下部分中的下载链接，下载 OLE DB Driver 的早期版本：

## <a name="1823"></a>18.2.3

![下载](../../ssms/media/download-icon.png)[下载 x64 安装程序](https://go.microsoft.com/fwlink/?linkid=2119554)  
![下载](../../ssms/media/download-icon.png)[下载 x86 安装程序](https://go.microsoft.com/fwlink/?linkid=2119738)  

发布日期：2019 年 6 月

如果想要安装的语言版本不包含在检测到的语言中，可以使用以下直接链接。  
对于 x64 驱动程序：[中文（简体）](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x804) | [中文（繁体）](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x404) | [英语（美国）](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x409) | [法语](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x40c) | [德语](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x407) | [意大利语](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x410) | [日语](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x411) | [朝鲜语](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x412) | [葡萄牙语（巴西）](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x416) | [俄语](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x419) | [西班牙语](https://go.microsoft.com/fwlink/?linkid=2119554&clcid=0x40a)  
对于 x86 驱动程序：[中文（简体）](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x804) | [中文（繁体）](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x404) | [英语（美国）](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x409) | [法语](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x40c) | [德语](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x407) | [意大利语](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x410) | [日语](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x411) | [朝鲜语](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x412) | [葡萄牙语（巴西）](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x416) | [俄语](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x419) | [西班牙语](https://go.microsoft.com/fwlink/?linkid=2119738&clcid=0x40a)  

### <a name="features-added-in-1823"></a>18.2.3 中的新增功能

| 新增功能 | 详细信息 |
| :------------ | :------ |
| 支持从 SQL Server 可移动媒体升级驱动程序。 | 借助此改进，可以直接从 SQL Server 可移动媒体升级驱动程序。 |
| &nbsp; | &nbsp; |

## <a name="1822"></a>18.2.2

![下载](../../ssms/media/download-icon.png)[下载 x64 安装程序](https://go.microsoft.com/fwlink/?linkid=2118512)  
![下载](../../ssms/media/download-icon.png)[下载 x86 安装程序](https://go.microsoft.com/fwlink/?linkid=2118415)  

发布日期：2019 年 5 月

如果想要安装的语言版本不包含在检测到的语言中，可以使用以下直接链接。  
对于 x64 驱动程序：[中文（简体）](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x804) | [中文（繁体）](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x404) | [英语（美国）](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x409) | [法语](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x40c) | [德语](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x407) | [意大利语](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x410) | [日语](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x411) | [朝鲜语](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x412) | [葡萄牙语（巴西）](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x416) | [俄语](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x419) | [西班牙语](https://go.microsoft.com/fwlink/?linkid=2118512&clcid=0x40a)  
对于 x86 驱动程序：[中文（简体）](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x804) | [中文（繁体）](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x404) | [英语（美国）](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x409) | [法语](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x40c) | [德语](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x407) | [意大利语](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x410) | [日语](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x411) | [朝鲜语](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x412) | [葡萄牙语（巴西）](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x416) | [俄语](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x419) | [西班牙语](https://go.microsoft.com/fwlink/?linkid=2118415&clcid=0x40a)  

### <a name="bugs-fixed-in-1822"></a>已在 18.2.2 中修复的 bug

| 已修复 bug | 详细信息 |
| :-------- | :------ |
| 已修复多线程单元 (MTA) 中的非交互式 Azure Active Directory 身份验证。 | OLE DB 驱动程序 18.2.1 错误地尝试更改之前初始化为多线程的单元 (MTA) 上的 COM 并发模型。 因此，在调用 [IDBInitialize::Initialize](https://go.microsoft.com/fwlink/?linkid=2092522) 接口前，在对 [CoInitialize](https://go.microsoft.com/fwlink/?linkid=2092520) 或 [CoInitializeEx](https://go.microsoft.com/fwlink/?linkid=2092521) 发出一个以上的后续调用的应用程序中，使用任何 Azure Active Directory 身份验证模式时，该驱动程序都会连接失败。 |
| &nbsp; | &nbsp; |

## <a name="1821"></a>18.2.1

![下载](../../ssms/media/download-icon.png)[下载 x64 安装程序](https://go.microsoft.com/fwlink/?linkid=2118511)  
![下载](../../ssms/media/download-icon.png)[下载 x86 安装程序](https://go.microsoft.com/fwlink/?linkid=2118278)  

发布日期：2019 年 2 月

如果想要安装的语言版本不包含在检测到的语言中，可以使用以下直接链接。  
对于 x64 驱动程序：[中文（简体）](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x804) | [中文（繁体）](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x404) | [英语（美国）](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x409) | [法语](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x40c) | [德语](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x407) | [意大利语](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x410) | [日语](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x411) | [朝鲜语](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x412) | [葡萄牙语（巴西）](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x416) | [俄语](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x419) | [西班牙语](https://go.microsoft.com/fwlink/?linkid=2118511&clcid=0x40a)  
对于 x86 驱动程序：[中文（简体）](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x804) | [中文（繁体）](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x404) | [英语（美国）](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x409) | [法语](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x40c) | [德语](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x407) | [意大利语](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x410) | [日语](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x411) | [朝鲜语](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x412) | [葡萄牙语（巴西）](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x416) | [俄语](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x419) | [西班牙语](https://go.microsoft.com/fwlink/?linkid=2118278&clcid=0x40a)  

### <a name="features-added-in-1821"></a>18.2.1 中的新增功能

| 新增功能 | 详细信息 |
| :------------ | :------ |
| 支持 UTF-8 服务器编码。 | [OLE DB Driver for SQL Server 中的 UTF-8 支持](features/utf-8-support-in-oledb-driver-for-sql-server.md)。 |
| Azure Active Directory 身份验证支持。 | [使用 Azure Active Directory](features/using-azure-active-directory.md)。 |
| &nbsp; | &nbsp; |

## <a name="1810"></a>18.1.0

![下载](../../ssms/media/download-icon.png)[下载 x64 安装程序](https://go.microsoft.com/fwlink/?linkid=2118506)  
![下载](../../ssms/media/download-icon.png)[下载 x86 安装程序](https://go.microsoft.com/fwlink/?linkid=2118509)  

发布日期：2018 年 7 月

如果想要安装的语言版本不包含在检测到的语言中，可以使用以下直接链接。  
对于 x64 驱动程序：[中文（简体）](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x804) | [中文（繁体）](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x404) | [英语（美国）](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x409) | [法语](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x40c) | [德语](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x407) | [意大利语](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x410) | [日语](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x411) | [朝鲜语](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x412) | [葡萄牙语（巴西）](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x416) | [俄语](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x419) | [西班牙语](https://go.microsoft.com/fwlink/?linkid=2118506&clcid=0x40a)  
对于 x86 驱动程序：[中文（简体）](https://go.microsoft.com/fwlink/?linkid=2118509&2118509=0x804) | [中文（繁体）](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x404) | [英语（美国）](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x409) | [法语](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x40c) | [德语](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x407) | [意大利语](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x410) | [日语](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x411) | [朝鲜语](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x412) | [葡萄牙语（巴西）](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x416) | [俄语](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x419) | [西班牙语](https://go.microsoft.com/fwlink/?linkid=2118509&clcid=0x40a)  

### <a name="features-added-in-1810"></a>18.1.0 中的新增功能

| 新增功能 | 详细信息 |
| :------------ | :------ |
| 对 `UseFMTONLY` 连接字符串密钥以及 `SSPROP_INIT_USEFMTONLY` 初始化属性的支持。 | 连接到 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 及更新版本时，`UseFMTONLY` 会控制检索元数据的方式。<br/><br/>有关详细信息，请参阅：[结合使用连接字符串关键字和 OLE DB Driver for SQL Server](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)。 |
| &nbsp; | &nbsp; |

### <a name="bugs-fixed-in-1810"></a>已在 18.1.0 中修复的 bug

| 已修复 bug | 详细信息 |
| :-------- | :------ |
| 已修复 BCP 格式化文件的错误版本。 | OLE DB 驱动程序 18.0 错误地将 BCP 格式化文件的版本设为 18.0，而不是 11.0。<br/>OLE DB 驱动程序 18.0 生成的格式文件无法由 OLE DB 驱动程序 18.1 读取。<br/>如果需要通过新的驱动程序使用以前版本的驱动程序生成的格式文件，则可以手动编辑文件以将版本更改为 11.0。 |
| &nbsp; | &nbsp; |

## <a name="1802"></a>18.0.2

![下载](../../ssms/media/download-icon.png)[下载 x64 安装程序](https://go.microsoft.com/fwlink/?linkid=2118504)  
![下载](../../ssms/media/download-icon.png)[下载 x86 安装程序](https://go.microsoft.com/fwlink/?linkid=2118277)  

发布日期：2018 年 3月

如果想要安装的语言版本不包含在检测到的语言中，可以使用以下直接链接。  
对于 x64 驱动程序：[中文（简体）](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x804) | [中文（繁体）](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x404) | [英语（美国）](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x409) | [法语](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x40c) | [德语](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x407) | [意大利语](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x410) | [日语](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x411) | [朝鲜语](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x412) | [葡萄牙语（巴西）](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x416) | [俄语](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x419) | [西班牙语](https://go.microsoft.com/fwlink/?linkid=2118504&clcid=0x40a)  
对于 x86 驱动程序：[中文（简体）](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x804) | [中文（繁体）](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x404) | [英语（美国）](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x409) | [法语](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x40c) | [德语](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x407) | [意大利语](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x410) | [日语](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x411) | [朝鲜语](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x412) | [葡萄牙语（巴西）](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x416) | [俄语](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x419) | [西班牙语](https://go.microsoft.com/fwlink/?linkid=2118277&clcid=0x40a)  

### <a name="features-added-in-1802"></a>18.0.2 中的新增功能

| 新增功能 | 详细信息 |
| :------------ | :------ |
| 对 `MultiSubnetFailover` 连接字符串密钥以及 `SSPROP_INIT_MULTISUBNETFAILOVER` 初始化属性的支持。 | 有关详细信息，请参阅：<br/>&bull; &nbsp; [OLE DB Driver for SQL Server 支持高可用性和灾难恢复](features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)。<br/>&bull; &nbsp; [结合使用连接字符串关键字和 OLE DB Driver for SQL Server](applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md)。 |
| &nbsp; | &nbsp; |

## <a name="see-also"></a>另请参阅

[适用于 SQL Server 的 Microsoft OLE DB 驱动程序](oledb-driver-for-sql-server.md)
