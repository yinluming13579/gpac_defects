Affected Version:
gpac 2.2.1 0ff40625b602590afffb383ab03d155e0ba509ed(Current latest commit)

Vulnerability Description:
This defect represents a Use-After-Free (UAF) vulnerability, occurring at line 1047 in the file "/gpac/src/filters/dasher.c". This vulnerability could potentially be exploited maliciously, leading to a denial-of-service (DoS) attack.

gpac download address:
https://hub.fgit.cf/gpac/gpac.git

Defect Location and Description:


In the "dasher_configure_pid" function in the "/gpac/src/filters/dasher.c" file, a pointer variable named p is defined. This variable is passed to the gf_filter_pid_set_property function at line 1003 of the program, as illustrated in the following diagram.

![image](https://github.com/yinluming13579/gpac_defects/blob/main/gpac_6.png)


In the gf_filter_pid_set_property function, the pointer p corresponds to the variable named value. This variable, as a parameter, is passed into the gf_filter_pid_set_property_full function, as shown in the following diagram.

![image](https://github.com/yinluming13579/gpac_defects/blob/main/gpac_7.png)

In the gf_filter_pid_set_property_full function, the memory block pointed to by value->value.string is released at line 5627, as depicted in the following diagram.

![image](https://github.com/yinluming13579/gpac_defects/blob/main/gpac_8.png)


After the release of p->value.string, the program assigns the now-null pointer p->value.string to segext at line 1004. Subsequently, at line 1047, the strcmp function is called using the segext variable, leading to a null pointer dereference defect, as illustrated in the following diagram.

![image](https://github.com/yinluming13579/gpac_defects/blob/main/gpac_9.png)
