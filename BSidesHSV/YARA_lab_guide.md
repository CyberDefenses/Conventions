# "anti" checks
# packer attributes

As mentioned in the presentation, providing the 18 months worth of YARA research we had done was ... not really allowed.  As a compromise, a high level breakdown the logic agreed as acceptable.  That outline is included below.  Anyone that is a fan of YARA and gone through at least one of our (CDI) classes should have no problem re-creating the YARA to make the identification steps work.

##

## Anti-debugging checks
* IsDebuggerPresent
* CheckRemoteDebuggerPresent
* IsDebugged - hint:  Process Environement Block (BeingDebugged)
* NtGlobalFlags - hint: Process Environement Block (NtGlobalFlag)
* QueryInformationProcess - hint: NtQueryInformationProcess (ProcessDebugPort or ProcessDebugFlags or ProcessDebugObject)
* SetInformationThread - hint: NtSetInformationThread (HideThreadFromDebugger)
* DebugActiveProcess
* QueryPerformanceCounter
* GetTickCount
* OutputDebugString - hint: OutputDebugString (GetLastError())
* SetUnhandledExceptionFilter - hint: "kernel32.dll","UnhandledExceptionFilter"
* GenerateConsoleCtrlEvent
* SetConsoleCtrlHandler
* SetThreadContext
* Raise Exception - hint: "kernel32.dll","RaiseException"
* __invoke__watson - hint: SEH / GetThreadContext
* ____except__handler3 - hint: SEH / GetThreadContext
* ____except__handler4 - hint: SEH / GetThreadContext
* ____local__unwind3 - hint: SEH / GetThreadContext
* ____local__unwind4 - hint: SEH / GetThreadContext
* vbaExceptHandler - hint: SEH / GetThreadContext
* __XcptFilter - hint: SEH / GetThreadContext
* AddVectoredExceptionHandler - hint: SEH / GetThreadContext
* RemoveVectoredExceptionHandler - hint: SEH / GetThreadContext
* rdtsc instruction, which returns the processor time stamp
* Checks for common sandbox dlls (sbiedll.dll, dbghelp.dll, etc.)
* Sandbox checks (QEMU, VBox, VMWare, etc.)
* Checks for WINE
* Anti-debug process memory working set size, e.g., "kernel32.dll", "K32GetProcessMemoryInfo" and "kernel32.dll", "GetCurrentProcess"
* Presence of known debug tools, e.g., ollydbg.exe or winhex.exe

## Anti-VM
* Binary Tricks - hint: in Hex, like {56 4D 58 68} or {45 C7 00 01}
* Checks for common VM strings, e.g., Prod_VMware_Virtual_ or VBoxTray
* Checks for Common VM MAC addresses
* Drive Size checks
* File Path checks
* Common Sandbox User names
* WMI Video card checks
* checks for Bios version
* Count of processors
* Sandbox known product IDs
* Keyboard layout
* Registry Constants

## Anti-Sandbox
* rdtsc instruction - hint: GetProcessHeap & CloseHandle
* Sleep
* SetTimer
* WaitForSingleObject
* WaitForMultipleObjects

## Crypto Constants 
* Hash constants, e.g., MD5, SHA1
* Common Crypto (Blowfish, Whirlpool, etc.)

## Disabling
* AV disabling checks
* Disable User Access Control
* Disable Firewall
* Disable Registry
* Disable DEP
* Disable Task Manager

## Creation
* New Process Creation
* New Service Creation
* Install for autorun at Windows startup
* Create a COM server

## Injection
* Thread Injection
* Inject certificate into store

## Hijack
* Hijack network configuration
* Steal local credential

## Communication
* Communications over UDP network
* Listen for incoming communication
* SMTP Communication
* P2P network communication
* TOR communication
* IRC communication
* HTTP communication
* Communications over FTP
* Communications over Raw Socket
* Communications use DNS
* Communications use SSL
* Communication using dga

## Packer Attributes

* Entropy checks (portioned, sectioned, orthogonal, etc.)
* Compile Checks
* Data beyond ImageSize
* Import Table Checks
* Export Table Checks
* PE/DOS header checks

## Compression Checks
* Section Merging
* Byte Stomping
* Byte re-use
* Byte Scavenging

## Anti-Analysis
* Fake code to fool identification (usually strings)
* ... more

## Protection
* Token check
* Fingerprinting
* Integrity check

## Anti-Dumping
* API hooking
* ... more

## Anti-emulation
* OpCodes
* ... more



