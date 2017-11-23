---
title: "了解游标类型 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4f4d3db7-4f76-450d-ab63-141237a4f034
caps.latest.revision: "51"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dfd697881fbde24c797707990d53c2cc33576a24
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="understanding-cursor-types"></a>了解游标类型
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  关系数据库中的操作会对整个行集起作用。 由 SELECT 语句返回的行集包括满足该语句的 WHERE 子句中条件的所有行。 这种由语句返回的完整行集称为结果集。 应用程序并不总能将整个结果集作为一个单元来有效地处理。 这些应用程序需要一种机制以便每次处理一行或一部分行。 游标就是提供这种机制的对结果集的一种扩展。  
  
 游标通过执行以下操作来扩展结果集处理：  
  
-   允许定位在结果集的特定行。  
  
-   从结果集的当前位置检索一行或一部分行。  
  
-   支持数据设置到结果中的当前位置处的行的修改。  
  
-   为由其他用户对显示在结果集中的数据库数据所做的更改提供不同级别的可见性支持。  
  
> [!NOTE]  
>  有关完整说明[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]游标类型，请参阅中的"游标类型 （数据库引擎）"主题[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]联机丛书。  
  
 JDBC 规范支持的只进和可滚动游标对其他作业所做的更改可能敏感，也可能不敏感，而且可以是只读游标或可更新游标。 此功能由[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)类。  
  
## <a name="remarks"></a>注释  
 JDBC 驱动程序支持以下游标类型：  
  
|结果集<br /><br /> （游标）类型|SQL Server 游标类型|特征|select<br /><br /> 方法|响应<br /><br /> 缓冲|Description|  
|------------------------------------|----------------------------|---------------------|-----------------------|----------------------------|-----------------|  
|TYPE_FORWARD_ONLY (CONCUR_READ_ONLY)|N/A|只进，只读|直接|full|应用程序必须（向前）经过结果集一次。 这是默认行为，其行为与 TYPE_SS_DIRECT_FORWARD_ONLY 游标的方式相同。 在语句执行期间，驱动程序将整个结果集从服务器读入内存中。|  
|TYPE_FORWARD_ONLY (CONCUR_READ_ONLY)|N/A|只进，只读|直接|自适应|应用程序必须（向前）经过结果集一次。 其行为与 TYPE_SS_DIRECT_FORWARD_ONLY 游标的行为相同。 当应用程序请求行时，驱动程序从服务器读取对应的行，这样可以最大限度地减少客户端内存占用。|  
|TYPE_FORWARD_ONLY (CONCUR_READ_ONLY)|快进|只进，只读|cursor|N/A|应用程序必须通过使用服务器游标在结果集中进行一次（前进）传递。 其行为与 TYPE_SS_SERVER_CURSOR_FORWARD_ONLY 游标的行为相同。<br /><br /> 从提取大小指定的服务器中分块检索行。|  
|TYPE_FORWARD_ONLY (CONCUR_UPDATABLE)|动态（只进）|只进，可更新|N/A|N/A|应用程序必须（向前）经过结果集一次才能更新一行或多行。<br /><br /> 从提取大小指定的服务器中分块检索行。<br /><br /> 默认情况下，当应用程序调用提取大小固定[setFetchSize](../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md)方法[SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md)对象。<br /><br /> **注意：** JDBC 驱动程序提供一种自适应缓冲功能，允许您检索语句执行结果从[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]随着应用程序需要它们，而不是一次。 例如，如果应用程序需要检索一个因为太大而无法完全容纳于应用程序内存中的大型数据块，则自适应缓冲使客户端应用程序可以检索诸如流这样的值。 该驱动程序的默认行为是"**自适应**"。 但是，若要实现的只进的可更新结果集的自适应缓冲，则应用程序必须显式调用[setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)方法[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)对象通过提供**字符串**值"**自适应"**。 有关代码示例，请参阅[更新大型数据示例](../../connect/jdbc/updating-large-data-sample.md)。|  
|TYPE_SCROLL_INSENSITIVE|静态|可滚动，不可更新。<br /><br /> 外部行更新、插入和删除不可见。|N/A|N/A|应用程序需要数据库快照。 结果集不可更新。 仅支持 CONCUR_READ_ONLY。  使用此游标类型时，所有其他并发类型都将导致异常。<br /><br /> 从提取大小指定的服务器中分块检索行。|  
|TYPE_SCROLL_SENSITIVE<br /><br /> (CONCUR_READ_ONLY)|Keyset|可滚动，只读的。 外部行更新可见，删除显示为缺失数据。<br /><br /> 外部行插入不可见。|N/A|N/A|该应用程序以查看更改后的数据只是现有的行。<br /><br /> 从提取大小指定的服务器中分块检索行。|  
|TYPE_SCROLL_SENSITIVE<br /><br /> （CONCUR_UPDATABLE、CONCUR_SS_SCROLL_LOCKS、CONCUR_SS_OPTIMISTIC_CC、CONCUR_SS_OPTIMISTIC_CCVAL）|Keyset|可滚动，可更新。<br /><br /> 外部和内部行更新可见，删除显示为缺失数据；插入不可见。|N/A|N/A|应用程序可以通过使用结果集对象来更改现有行中的数据。 应用程序还必须能够查看对行之外的结果集对象从的人所做的更改。<br /><br /> 从提取大小指定的服务器中分块检索行。|  
|TYPE_SS_DIRECT_FORWARD_ONLY|N/A|只进，只读|N/A|full 或 adaptive|整数值 = 2003。 提供一个完全缓冲的只读客户端游标。 不创建服务器游标。<br /><br /> 仅支持 CONCUR_READ_ONLY 并发类型。 所有其他并发类型导致与此游标类型一起使用时引发异常。|  
|TYPE_SS_SERVER_CURSOR_FORWARD_ONLY|快进|只进|N/A|N/A|整数值 = 2004。 快速，使用服务器游标访问所有数据。 使用 CONCUR_UPDATABLE 并发类型时可更新。<br /><br /> 从提取大小指定的服务器中分块检索行。<br /><br /> 若要实现这种情况下的自适应缓冲，则应用程序必须显式调用[setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)方法[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)对象提供**字符串**值"**自适应"**。 有关代码示例，请参阅[更新大型数据示例](../../connect/jdbc/updating-large-data-sample.md)。|  
|TYPE_SS_SCROLL_STATIC|静态|不反映其他用户的更新。|N/A|N/A|整数值 = 1004。 应用程序需要数据库快照。 这是[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-特定同义词 JDBC TYPE_SCROLL_INSENSITIVE，并具有相同的并发设置行为。<br /><br /> 从提取大小指定的服务器中分块检索行。|  
|TYPE_SS_SCROLL_KEYSET<br /><br /> (CONCUR_READ_ONLY)|Keyset|可滚动，只读。 外部行更新可见，删除显示为缺失数据。<br /><br /> 外部行插入不可见。|N/A|N/A|整数值 = 1005。 应用程序必须只看到现有行的已更改数据。 这是[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-特定同义词 JDBC TYPE_SCROLL_SENSITIVE，并具有相同的并发设置行为。<br /><br /> 从提取大小指定的服务器中分块检索行。|  
|TYPE_SS_SCROLL_KEYSET<br /><br /> （CONCUR_UPDATABLE、CONCUR_SS_SCROLL_LOCKS、CONCUR_SS_OPTIMISTIC_CC、CONCUR_SS_OPTIMISTIC_CCVAL）|Keyset|可滚动，可更新。<br /><br /> 外部和内部行更新可见，删除显示为缺失数据；插入不可见。|N/A|N/A|整数值 = 1005。 应用程序必须更改现有行的数据或看到现有行的已更改数据。 这是[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-特定同义词 JDBC TYPE_SCROLL_SENSITIVE，并具有相同的并发设置行为。<br /><br /> 从提取大小指定的服务器中分块检索行。|  
|TYPE_SS_SCROLL_DYNAMIC<br /><br /> (CONCUR_READ_ONLY)|Dynamic|可滚动，只读的。<br /><br /> 外部行更新和插入可见，删除显示为当前提取缓冲区中的临时缺失数据。|N/A|N/A|整数值 = 1006。 应用程序在游标的生存期内必须看到现有行的已更改数据并看到已插入和已删除的行。<br /><br /> 从提取大小指定的服务器中分块检索行。|  
|TYPE_SS_SCROLL_DYNAMIC<br /><br /> （CONCUR_UPDATABLE、CONCUR_SS_SCROLL_LOCKS、CONCUR_SS_OPTIMISTIC_CC、CONCUR_SS_OPTIMISTIC_CCVAL）|Dynamic|可滚动，可更新。<br /><br /> 外部和内部行更新和插入可见，删除显示为当前提取缓冲区中的临时缺失数据。|N/A|N/A|整数值 = 1006。 应用程序可能更改现有行的数据或插入或删除的行使用结果集对象。 应用程序还必须能够看到更改、 插入和删除其他人所做从结果集中对象以外的区域。<br /><br /> 从提取大小指定的服务器中分块检索行。|  
  
## <a name="cursor-positioning"></a>游标定位  
 仅支持 TYPE_FORWARD_ONLY、 TYPE_SS_DIRECT_FORWARD_ONLY 和 TYPE_SS_SERVER_CURSOR_FORWARD_ONLY 游标[下一步](../../connect/jdbc/reference/next-method-sqlserverresultset.md)定位方法。  
  
 TYPE_SS_SCROLL_DYNAMIC 游标不支持[绝对](../../connect/jdbc/reference/absolute-method-sqlserverresultset.md)和[getRow](../../connect/jdbc/reference/getrow-method-sqlserverresultset.md)方法。 可以通过对的调用的组合近似绝对方法[第一个](../../connect/jdbc/reference/first-method-sqlserverresultset.md)和[相对](../../connect/jdbc/reference/relative-method-sqlserverresultset.md)动态游标的方法。  
  
 GetRow 方法所 TYPE_FORWARD_ONLY、 TYPE_SS_DIRECT_FORWARD_ONLY、 TYPE_SS_SERVER_CURSOR_FORWARD_ONLY、 TYPE_SS_SCROLL_KEYSET 和 TYPE_SS_SCROLL_STATIC 游标支持。 所有的只进游标类型具有的 getRow 方法返回通过游标中到目前为止读取的行数。  
  
> [!NOTE]  
>  当应用程序进行定位或 getRow 方法不支持的调用的不支持的游标时，引发异常并显示消息，"请求的操作不支持此游标类型。"  
  
 仅 TYPE_SS_SCROLL_KEYSET 和等效的 TYPE_SCROLL_SENSITIVE 游标才显示已删除的行。 如果光标定位在已删除的行，列的值都不可用，和[rowDeleted](../../connect/jdbc/reference/rowdeleted-method-sqlserverresultset.md)方法返回"true"。 调用以获取\<类型 > 方法引发异常，消息、"无法获得值从已删除行"。 无法更新已删除的行。 如果你尝试调用更新\<类型 > 已删除的行的方法，并显示消息将引发异常，"已删除的行不能更新时间"。 TYPE_SS_SCROLL_DYNAMIC 游标具有这种相同的行为，直到将此游标移出当前提取缓冲区之外。  
  
 前进游标和动态游标以类似的方式显示已删除的行，但仅限仍可在提取缓冲区中访问游标的情况。 对于前进游标，这一点相当简单。 对于动态游标，当提取大小大于 1 时，这一点就变得较复杂了。 应用程序可以在由提取缓冲区定义的窗口内前后移动游标，但是，当离开在其中更新已删除行的原始提取缓冲区时，已删除的行将消失。 如果应用程序并不希望通过使用动态游标来查看临时删除的行，则应使用 Fetch Relative (0)。  
  
 如果使用游标更新 TYPE_SS_SCROLL_KEYSET 或 TYPE_SCROLL_SENSITIVE 游标行的键值，则行将保持其在结果集中的原始位置，无论已更新的行是否符合游标的选择条件。 如果在游标之外更新行，则已删除的行将出现在该行的原始位置，然而，该行仅当游标中存在具有新键值的另一行但它先前已被删除时才会出现在游标中。  
  
 对于动态游标，已更新的行将保留其在提取缓冲区的位置，直到离开由提取缓冲区定义的窗口。 已更新的行随后可能重新出现在结果集内的不同位置，或者可能完全消失。 必须避免结果集中出现临时不一致的应用程序所使用的提取大小应为 1（对于 CONCUR_SS_SCROLL_LOCKS 并发机制，默认值为 8 行；对于其他并发机制，则为 128 行）。  
  
## <a name="cursor-conversion"></a>游标转换  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]有时可以选择实现游标类型不是请求，这被称为隐式游标转换 （或游标降级）。 有关隐式游标转换的详细信息，请参阅中的"使用隐式游标转换"主题[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]联机丛书。  
  
 与[!INCLUDE[ssVersion2000](../../includes/ssversion2000_md.md)]，当你更新通过 ResultSet.TYPE_SCROLL_SENSITIVE 和 ResultSet.CONCUR_UPDATABLE 结果的数据设置，将引发异常的消息"游标只读"。 发生此异常的原因[!INCLUDE[ssVersion2000](../../includes/ssversion2000_md.md)]完成隐式游标转换为该结果设置并在未返回已请求的可更新光标。  
  
 若要解决此问题，可以采用以下两种解决方案之一：  
  
-   确保基础表具有主键  
  
-   使用[SQLServerResultSet.TYPE_SS_SCROLL_DYNAMIC](../../connect/jdbc/reference/type-ss-scroll-dynamic-field-sqlserverresultset.md)而不是创建一条语句时 ResultSet.TYPE_SCROLL_SENSITIVE。  
  
## <a name="cursor-updating"></a>游标更新  
 对于游标而言，如果游标类型和并发支持更新，则支持对游标进行就地更新。 如果光标未定位在结果集中的可更新行 (没有 get\<类型 > 方法调用成功)，对更新的调用\<类型 > 方法会引发异常，消息，"结果集都有没有当前行"。 JDBC 规范规定，对类型为 CONCUR_READ_ONLY 的游标的列调用 update 方法时，将引发异常。 在其中行是不可更新，例如由于如竞争更新或删除开放式并发冲突的情况下，该异常，可能不会出现直到[insertRow](../../connect/jdbc/reference/insertrow-method-sqlserverresultset.md)， [updateRow](../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md)，或[deleteRow](../../connect/jdbc/reference/deleterow-method-sqlserverresultset.md)调用。  
  
 调用以更新后\<类型 >，受影响的列不能由 get 访问\<类型 > 直到 updateRow 或[cancelRowUpdates](../../connect/jdbc/reference/cancelrowupdates-method-sqlserverresultset.md)已调用。 这将避免以下问题：使用与服务器返回的类型不同的类型更新列，而随后调用的 getter 可能会引起给出不准确结果的客户端类型转换。 调用以获取\<类型 > 将引发异常，消息、"updateRow() 之前，无法访问已更新列或已调用 cancelRowUpdates()。"  
  
> [!NOTE]  
>  如果没有列已更新，调用 updateRow 方法，JDBC 驱动程序将引发异常，消息、"updateRow() 调用时没有列已更新。"  
  
 后[moveToInsertRow](../../connect/jdbc/reference/movetoinsertrow-method-sqlserverresultset.md)已被调用，将引发异常如果以外的其他任何方法获取\<类型 >，更新\<类型 >，insertRow，和光标定位方法 (包括[moveToCurrentRow](../../connect/jdbc/reference/movetocurrentrow-method-sqlserverresultset.md)) 对结果集调用。 MoveToInsertRow 方法有效地将结果放置于设置到在插入模式和光标定位方法终止在插入模式。 相对光标定位调用相对于调用 moveToInsertRow 之前的时间位置来移动光标。 在游标定位调用之后，最终的目标游标位置将成为新的游标位置。  
  
 如果光标定位在插入模式将不会成功时所做的调用，调用了 moveToInsetRow 之前的原始光标位置，则失败的调用之后的光标位置。 如果 insertRow 失败，光标会保持在插入行并且光标保留在插入模式。  
  
 位于插入行中的列最初处于未初始化状态。 调用更新\<类型 > 方法列将状态设置为初始化。 Get 调用\<类型 > 未经初始化即列方法将引发异常。 InsertRow 方法的调用返回到未初始化状态中插入行的所有列。  
  
 如果调用 insertRow 方法时，任何列都未初始化，将插入列的默认值。 如果没有默认值而列可为 Null，则插入 NULL。 如果没有默认值且列不可为 Null，服务器将返回错误，此时将引发异常。  
  
> [!NOTE]  
>  对 getRow 方法的调用返回在插入模式下的 0。  
>   
>  JDBC 驱动程序不支持定位更新或删除。 根据 JDBC 规范[setCursorName](../../connect/jdbc/reference/setcursorname-method-sqlserverstatement.md)方法不起作用和[getCursorName](../../connect/jdbc/reference/getcursorname-method-sqlserverresultset.md)方法将引发异常，如果调用。  
>   
>  只读和静态游标始终无法更新。  
>   
>  SQL Server 将服务器游标限制到单一结果集中。 如果批处理或存储过程包含多条语句，则必须使用只进只读客户端游标。  
  
## <a name="see-also"></a>另请参阅  
 [通过 JDBC 驱动程序管理结果集](../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md)  
  
  
