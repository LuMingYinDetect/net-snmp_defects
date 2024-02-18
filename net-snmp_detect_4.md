Affected Version:
net-snmp 5.9 75f2aedd88ff0d42a99bd2e29aed749012334bad

Vulnerability Description:
The vulnerability is a memory leak bug located at line 320 of the file /net-snmp/apps/snmpvacm.c. This vulnerability could potentially be exploited maliciously to cause resource exhaustion and denial of service attacks.

net-snmp download address:
https://github.com/net-snmp/net-snmp.git

Defect details:

1.A pointer named pdu is defined at line 252 of the file /net-snmp/apps/snmpvacm.c. The program assigns the return value of the snmp_pdu_create function to pdu at line 315, as shown in the figure below:

![image](https://github.com/LuMingYinDetect/net-snmp_defects/blob/main/net-snmp_1.png)

2.At line 134 of the snmp_pdu_create function, a dynamic memory area is allocated using the calloc function. This allocated memory area is returned at line 149, as shown in the figure below:

![image](https://github.com/LuMingYinDetect/net-snmp_defects/blob/main/net-snmp_2.png)

3.After allocating a memory area for pdu at line 315, if the conditional statement at line 317 evaluates to true, the program will jump to the close_session label at line 320, as shown in the figure below:

![image](https://github.com/LuMingYinDetect/net-snmp_defects/blob/main/net-snmp_3.png)

4.In the subsequent code following the close_session label, there is no deallocation of the memory area pointed to by pdu, which constitutes a memory leak defect, as shown in the figure below:

![image](https://github.com/LuMingYinDetect/net-snmp_defects/blob/main/net-snmp_4.png)
