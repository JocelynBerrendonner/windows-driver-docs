---
title: D3dCreateSurfaceEx Handles and Flip
description: D3dCreateSurfaceEx Handles and Flip
ms.assetid: b87762fd-444d-437a-b076-189f51cc6dd1
keywords: ["context WDK Direct3D , D3dCreateSurfaceEx", "D3dCreateSurfaceEx", "flipping WDK Direct3D", "DdFlip"]
---

# D3dCreateSurfaceEx Handles and Flip


## <span id="ddk_d3dcreatesurfaceex_handles_and_flip_gg"></span><span id="DDK_D3DCREATESURFACEEX_HANDLES_AND_FLIP_GG"></span>


DirectDraw surface structures are designed to represent conceptual surfaces, not necessarily specific locations in video memory. The main usage of this abstraction is in a primary flipping chain, where the application uses one constant surface object to represent the back buffer, even though the back buffer may be moving around in video memory as a result of the [*DdFlip*](https://msdn.microsoft.com/library/windows/hardware/ff549306) function.

The [*DdFlip*](https://msdn.microsoft.com/library/windows/hardware/ff549306) function takes a ring of surfaces, and sequentially reassigns their video memory pointers around this ring. In the particular case of two surface objects, the process is reduced to trading their video memory pointers. In addition, the DirectDraw runtime also rotates the [**D3dCreateSurfaceEx**](https://msdn.microsoft.com/library/windows/hardware/ff542840) handles associated with each surface, and the driver-owned contents of the **dwReserved1** members of each surface. This behavior has some interesting consequences for a DirectX 7.0 driver, and effectively rules out the embedding of pointers to DirectDraw surface structures inside the driver's own surface structures.

Consider two surface objects, A and B, that have associated handles H<sub>A</sub> and H<sub>B</sub>, and **fpVidMem** (a member of the [**DD\_SURFACE\_GLOBAL**](https://msdn.microsoft.com/library/windows/hardware/ff551726) structure) values of F<sub>A</sub> and F<sub>B</sub>. Further, suppose that the application is using surface structure A to refer to the back buffer of a flipping chain. At [*DdFlip*](https://msdn.microsoft.com/library/windows/hardware/ff549306) time, the handles and both **fpVidMem** values are swapped, so that surface A has H<sub>B</sub> and F<sub>B</sub>, and surface B has H<sub>A</sub> and F<sub>A</sub>. The application now tries to draw to the back buffer, surface A, which should represent the video memory at F<sub>B</sub> (because the application initiated a call to *DdFlip*).

A drawing command is issued to the driver, which looks up the handle associated with that surface (which is now H<sub>B</sub>, not H<sub>A</sub>). What would happen if the driver merely stores a pointer to the DirectDraw surface structure? The driver looks up H<sub>B</sub>, then follows the stored pointer to surface B, which now has an **fpVidMem** value of F<sub>A</sub>. Drawing begins on the video memory at F<sub>A</sub>. This is not what the application is expecting. If, on the other hand, the driver stores surface data in its own structures, rather than following a pointer to the DirectDraw surface structure, then H<sub>B</sub> still resolves to F<sub>B</sub>, and drawing occurs on the correct surface. This latter case is the way the current DDI is implemented.

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[display\display]:%20D3dCreateSurfaceEx%20Handles%20and%20Flip%20%20RELEASE:%20%282/10/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")




