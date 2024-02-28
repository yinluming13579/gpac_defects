Affected Version:
gpac 2.2.1 0ff40625b602590afffb383ab03d155e0ba509ed(Current latest commit)

Vulnerability Description:
The vulnerability is a memory leak issue, where a local variable named "gfio_blob" in the gf_fileio_from_blob function is allocated memory but not released.

gpac download address:
https://github.com/gpac/gpac.git

Defect Location and Description:


The gf_fileio_from_blob function defines a pointer variable named gfio_blob. This pointer variable is passed to the GF_SAFEALLOC function to allocate a block of dynamic memory, as shown in the following diagram.

![image](https://github.com/yinluming13579/gpac_defects/blob/main/gpac_10.png)

In the gf_malloc function, a memory area is allocated for this pointer variable, as shown in the following figure.

![image](https://github.com/yinluming13579/gpac_defects/blob/main/gpac_11.png)

If the program returns a null pointer on line 1447 (instead of returning a res variable containing the gfio_blob pointer information on line 1451), the memory area pointed to by the gfio_blob pointer is not used and not released due to the program returning a null pointer, resulting in a memory leak vulnerability, as shown in the following figure.

![image](https://github.com/yinluming13579/gpac_defects/blob/main/gpac_12.png)
