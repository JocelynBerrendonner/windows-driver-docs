---
title: WIA Transfer Constants
author: windows-driver-content
description: WIA Transfer Constants
MS-HAID:
- 'WIA\_arch\_7a6af1c8-2e3b-457a-8837-359ef89e77f8.xml'
- 'image.wia\_transfer\_constants'
MSHAttr:
- 'PreferredSiteName:MSDN'
- 'PreferredLib:/library/windows/hardware'
ms.assetid: 69f76919-5bbb-4968-997c-2d51f19aab6b
---

# WIA Transfer Constants


This topic contains a list of the constants that are used for WIA **IStream**-based transfers.

These constants are divided into three subgroups:

-   Item type

-   Callback messages

-   Transfer flags

### Item Type

The following table shows which WIA item type bits relate to stream-based data transfer.

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>WiaItemTypeTransfer</strong></p></td>
<td><p>This [<strong>WIA_IPA_ITEM_FLAGS</strong>](https://msdn.microsoft.com/library/windows/hardware/ff551585) bit should be set on all items that are capable of transferring data; that is, an application can initiate a download or upload on items that have this bit set.</p></td>
</tr>
</tbody>
</table>

 

### Callback Messages

The following table shows possible values for the *lFlags* parameter of **IWiaTransferCallback::TransferCallback**.

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_TRANSFER_MSG_STATUS</p></td>
<td><p>Notifies the application of the progress of the transfer.</p>
<p><em>pWiaTransferParams</em>-&gt; <em>lPercentComplete</em> contains the percent complete for this item and the page that is being transferred.</p></td>
</tr>
<tr class="even">
<td><p>WIA_TRANSFER_MSG_END_OF_STREAM</p></td>
<td><p>Notifies the application that there is no more data to be transferred to the current data stream and that the stream may be closed.</p>
<p>A new stream may subsequently be requested in a multi-item or multipage transfer.</p>
<p>Drivers do not send this message manually--the WIA service will automatically send this message when the driver asks for the next stream.</p></td>
</tr>
<tr class="odd">
<td><p>WIA_TRANSFER_MSG_END_OF_TRANSFER</p></td>
<td><p>Received by the application at the end of the transfer.</p>
<p>The driver does not send this message--the WIA service will send this message automatically after the transfer has ended (that is, the call to <strong>IWiaMiniDrv::drvAcquiItemData</strong> returns).</p></td>
</tr>
<tr class="even">
<td><p>WIA_TRANSFER_MSG_ERROR</p></td>
<td><p>Reserved by Microsoft for future use.</p></td>
</tr>
<tr class="odd">
<td><p>WIA_TRANSFER_MSG_DEVICE_STATUS</p></td>
<td><p>Indicates an error during the transfer (for example, a paper jam).</p>
<p><em>pWiaTransferParams</em>-&gt;<em>hrErrorStatus</em> contains the error status code.</p></td>
</tr>
<tr class="even">
<td><p>WIA_TRANSFER_MSG_NEW_PAGE</p></td>
<td><p>Indicates that a new page is being transferred during a multipage transfer when a format that supports multiple pages in one file (such as multifile TIFF) is being used.</p></td>
</tr>
</tbody>
</table>

 

### Transfer Flags

The following table shows the flags that may be passed into [**IWiaMiniDrv::drvAcquireItemData**](https://msdn.microsoft.com/library/windows/hardware/ff543956).

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_MINIDRV_TRANSFER_DOWNLOAD</p></td>
<td><p>Indicates that the transfer is a stream-based download operation (that is, a data transfer from a device to an application).</p>
<p>Applications do not set this bit directly. The WIA service sets this bit if the application calls <strong>IWiaTransfer::Download</strong>.</p></td>
</tr>
<tr class="even">
<td><p>WIA_MINIDRV_TRANSFER_UPLOAD</p></td>
<td><p>Indicates that the transfer is a stream-based upload operation (that is, a data transfer from an application to a device).</p>
<p>Applications do not set this bit directly. The WIA service sets this bit if the application calls <strong>IWiaTransfer::Upload</strong>.</p></td>
</tr>
<tr class="odd">
<td><p>WIA_MINIDRV_TRANSFER_ACQUIRE_CHILDREN</p></td>
<td><p>Indicates that the driver should perform a folder transfer. If this value is called on a folder item, the application requests to transfer the children of that folder.</p>
<p>This value will be set if an application requests a folder transfer by setting the <em>lFlags</em> parameter of <strong>IWiaTransfer::Download</strong> to WIA _TRANSFER_ACQUIRE_CHILDREN <em>and</em> the driver has specified that it can transfer multiple children in one scan. If the driver cannot perform this type of transfer, the WIA service will make multiple calls into the driver and WIA_MINIDRV_TRANSFER_ACQUIRE_CHILDREN will <em>not</em> be set.</p></td>
</tr>
</tbody>
</table>

 

For more information about the **IWiaTransfer** and **IWiaTransferCallback** interfaces, see the Microsoft Windows SDK documentation.

 

 


--------------------
[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bimage\image%5D:%20WIA%20Transfer%20Constants%20%20RELEASE:%20%288/17/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")


