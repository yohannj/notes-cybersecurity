# Looking into resources

When seeing LoadString, e.g.
```c
void __noreturn start()
{
  CHAR Buffer[1028]; // [esp+0h] [ebp-4A0h] BYREF
  LPCSTR lpText; // [esp+404h] [ebp-9Ch]
  char v2[144]; // [esp+408h] [ebp-98h] BYREF
  HRSRC ResourceA; // [esp+498h] [ebp-8h]
  UINT uID; // [esp+49Ch] [ebp-4h]

  MD5::MD5((MD5 *)v2);
  memset(Buffer, 0, 1024);
  uID = 0;
  ResourceA = FindResourceA(0, "rc.rc", (LPCSTR)6);
  uID = 272;
  LoadStringA(0, 0x110u, Buffer, 1023);
  lpText = MD5::digestString((MD5 *)v2, Buffer);
  MessageBoxA(0, lpText, "We've been compromised!", 0x30u);
  ExitProcess(0);
}
```

One can load resources in IDA (at file loading) + use ctrl+s to go to resources.

But we can directly use Resource Hacker to read the resources in a easy way.
To know which resources to look at, in `LoadStringA(0, 0x110u, Buffer, 1023)`, 0x110 indicates the index at which the string being loaded is.
