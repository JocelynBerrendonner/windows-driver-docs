---
title: AllowTethering
description: AllowTethering
MSHAttr:
- 'PreferredSiteName:MSDN'
- 'PreferredLib:/library/windows/hardware'
ms.assetid: f9b92c46-5e0e-447a-b571-bf549e9a749d
---

# AllowTethering


The AllowTethering element specifies whether the user is always allowed, never allowed, or allowed after an entitlement check to use Internet sharing.

**Note**  
If this element is configured to allow after an entitlement check, you must specify a [DeviceNotificationHandler](devicenotificationhandler.md) in your app that will handle the entitlement check.

 

## <span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>Usage


``` syntax
<AllowTethering>
  text
</AllowTethering>
```

## <span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>Attributes


There are no attributes.

## <span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>Text value


A string indicating whether Internet sharing is always allowed, never allowed, or allowed after an entitlement check.

## <span id="Child_elements"></span><span id="child_elements"></span><span id="CHILD_ELEMENTS"></span>Child elements


There are no child elements.

## <span id="Parent_elements"></span><span id="parent_elements"></span><span id="PARENT_ELEMENTS"></span>Parent elements


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Element</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>[NetworkConfiguration](networkconfiguration.md)</p></td>
<td><p>Specifies the purchase and Internet mobile broadband profiles to be used or whether standard user can perform PIN unlock operations.</p></td>
</tr>
</tbody>
</table>

 

## <span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="name="AllowTethering" type="tns:TetheringAllowedType" minOccurs="0" />

<xs:simpleType name="TetheringAllowedType">  
  <xs:restriction base="xs:string">
    <xs:enumeration value="Never"/>
    <xs:enumeration value="Always"/>
    <xs:enumeration value="EntitlementCheckRequired"/>
  </xs:restriction>
</xs:simpleType>
```

## <span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>Remarks


This element is only applicable to Windows 8.1 and Windows 10.

The AllowTethering element is optional.

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bp_mb\p_mb%5D:%20AllowTethering%20%20RELEASE:%20%281/18/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




