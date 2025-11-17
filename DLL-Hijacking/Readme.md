# DLL-Hijacking For Escalation

## DLL Defenition
⇒&nbsp;&nbsp; Modern OS off the ability to reuse common code such as libraries across binaries  
⇒&nbsp;&nbsp; When and executeble is started a linker loads these dynamic libararies into the proccess memory space  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;→ In linux these libraries are called   `shared objects` (_.so_)  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;→ In windows they are known as `dynamic link libararies` (_.dll_)  
⇒&nbsp;&nbsp; Since this loading process happens dynamically upon execution, this introduces the possibility of an attaker to inject malicious code in the form of malicious.dll that is injected into the processes memory space and executed  

⇒&nbsp;&nbsp; There are two possible ways to attack the DLL surface area:  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;      1- Find a DLL used by the victims binary that the attacker can overwrite with malicious code  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;      2- Introduce a new malicious DLL and trick the default search order to load the malicious code instead of the original one   

## DLL Loading Process

⇒&nbsp;&nbsp; When a new process is started system loader loads a main module of an application as well as ntdll.dll library into the address space   
⇒&nbsp;&nbsp; Then it checks if there are any additional libraries needed by the program and if so they will also get loaded   

⇒&nbsp;&nbsp; How does system loader know where to look for these additional DLLs   

⇒&nbsp;&nbsp; In windows there is a defined DLL search order & when a specific library is needed system will look through all the places one by one until it finds the right module and load it into the requesting process memmory space   

⇒&nbsp;&nbsp; For desktop apps the order is as shown below      
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;      1- It will search for the DLL in the address space in memmory  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;      2- Then it will check known dlls by reviewing the registry key   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;      3- Then it'll check the application folder   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;      4- Then it'll check system folders  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;      5- Then windows system directory  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;      6- Then it'll check entire windows directory   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;      7- Then current directory  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;      8- Then all folders in enviroment variable path  

⇒&nbsp;&nbsp; Search order is as shown below:  
<img src="https://imgur.com/dCYZ3q7.png" height="65%" width="75%" alt="modified services Steps"/>

## Hijacking DLL search order

⇒ If we do not specify a full path when loading a dll, windows tries to to find the DLL via the search order below  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;      1- It will search for the DLL in the address space in memmory  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;      2- Then it will check known dlls by reviewing the registry key   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;      3- Then it'll check the application folder   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;      4- Then it'll check system folders  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;      5- Then windows system directory  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;      6- Then it'll check entire windows directory   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;      7- Then current directory  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;      8- Then all folders in enviroment variable path  
⇒ In this case an attacker can hijack the intended DLL by placing a malicious DLL in a position that has priority over the regular DLL   





