Affected Version:
gpac 2.2.1 0ff40625b602590afffb383ab03d155e0ba509ed(Current latest commit)

Vulnerability Description:
The vulnerability is a memory leak issue, where a local variable named "dst_props" in the gf_filter_pid_merge_properties_internal function is allocated memory but not released.

gpac download address:
https://hub.fgit.cf/gpac/gpac.git

Defect Location and Description:

In the gf_filter_pid_merge_properties_internal function, a pointer variable named dst_props is defined. This pointer variable is allocated a block of dynamic memory by the check_new_pid_props function at line 6101 of the program, as shown in the following figure.
![image](https://github.com/yinluming13579/gpac_defects/blob/main/gpac_1.png)

In the check_new_pid_props function, a pointer variable named map is allocated a block of memory by the gf_props_new function and returned, as illustrated in the figure below.
![image](https://github.com/yinluming13579/gpac_defects/blob/main/gpac_2.png)

In the gf_props_new function, the pointer variable map is allocated a block of memory by GF_SAFEALLOC and returned, as shown in the following diagram.
![image](https://github.com/yinluming13579/gpac_defects/blob/main/gpac_3.png)


The gf_malloc function calls the malloc function to allocate a memory block of a specified size, as illustrated in the following diagram.
![image](https://github.com/yinluming13579/gpac_defects/blob/main/gpac_4.png)

After the program completes the aforementioned memory allocation operation, the variable dst_props obtains a dynamically allocated memory region. However, at line 6131, the program returns without releasing the memory pointed to by dst_props, leading to a memory leak defect, as depicted in the following diagram.
![image](https://github.com/yinluming13579/gpac_defects/blob/main/gpac_5.png)
