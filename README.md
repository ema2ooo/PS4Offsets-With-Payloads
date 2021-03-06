# PS4Offsets & Payloads 1.76/4.05/4.55

<p align="center">
🔥 PS4Offsets ~ Use these offsets if you need to update yuor old payloads. 🔥
  <br>
  
  These Offsets are for 4.55 firmware.
  
``` 
//4.55 KERN
#define	KERN_XFAST_SYSCALL 0x3095D0
#define KERN_PROCESS_ASLR 0x1BA559
#define KERN_PRISON_0 0x10399B0
#define KERN_ROOTVNODE 0x21AFA30
#define KERN_PTRACE_CHECK 0x17D2C1

//Reading 4.55 kernel_base...
void* kernel_base = &((uint8_t*)__readmsr(0xC0000082))[-KERN_XFAST_SYSCALL];
uint8_t* kernel_ptr = (uint8_t*)kernel_base;
void** got_prison0 =   (void**)&kernel_ptr[KERN_PRISON_0];
void** got_rootvnode = (void**)&kernel_ptr[KERN_ROOTVNODE];

// sceSblACMgrIsSystemUcred
uint64_t *sonyCred = (uint64_t *)(((char *)td_ucred) + 96);
*sonyCred = 0xffffffffffffffff;
// sceSblACMgrGetDeviceAccessType
uint64_t *sceProcType = (uint64_t *)(((char *)td_ucred) + 88);
*sceProcType = 0x3801000000000013; // Max access
// sceSblACMgrHasSceProcessCapability
uint64_t *sceProcCap = (uint64_t *)(((char *)td_ucred) + 104);
*sceProcCap = 0xffffffffffffffff; // Sce Process

// debug settings FULL
kernelBase[0x1B6D086] |= 0x14;
kernelBase[0x1B6D0A9] |= 0x3;
kernelBase[0x1B6D0AA] |= 0x1;
kernelBase[0x1B6D0C8] |= 0x1;

// Disable write protection
*(uint32_t*)&kernelBase[0x4D70F7] = 0;
*(uint32_t*)&kernelBase[0x4D7F81] = 0;

//UART Enabler 4.55
*(char *)(kernel_base + 0x1997BC8) = 0;

//EAP Internal Partition Key
kernelBase[0x258CCD0]
```
# 5.01 Offsets

```

KERN_XFAST_SYSCALL 0x1C0 //5.01 https://twitter.com/C0rpVultra/status/992789973966512133
KERN_PRISON_0		0x10986A0 //5.01
KERN_ROOTVNODE		0x22C19F0 //5.01
KERN_PMAP_PROTECT	0x2E2D00
KERN_PMAP_PROTECT_P	0x2E2D44
KERN_PMAP_STORE		0x22CB4F0
KERN_REGMGR_SETINT	0x4F8940
DT_HASH_SEGMENT		0xB5EE20

// debug settings patches 5.01
*(char *)(kernel_base + 0x1CD0686) |= 0x14;
*(char *)(kernel_base + 0x1CD06A9) |= 3;
*(char *)(kernel_base + 0x1CD06AA) |= 1;
*(char *)(kernel_base + 0x1CD06C8) |= 1;

// debug menu error patches 5.01
*(uint32_t *)(kernel_base + 0x4F8C78) = 0;
*(uint32_t *)(kernel_base + 0x4F9D8C) = 0;

// target_id patches 5.01
*(uint16_t *)(kernel_base + 0x1CD068C) = 0x8101;
*(uint16_t *)(kernel_base + 0x236B7FC) = 0x8101;

// disable pfs signature 5.01
*(uint32_t *)(kernel_base + 0x6A2320) = 0x90C3C031;

// enable mmap of all SELF 5.01
*(uint8_t*)(kernel_base + 0x117B0) = 0xB0;
*(uint8_t*)(kernel_base + 0x117B1) = 0x01;
*(uint8_t*)(kernel_base + 0x117B2) = 0xC3;

*(uint8_t*)(kernel_base + 0x117C0) = 0xB0;
*(uint8_t*)(kernel_base + 0x117C1) = 0x01;
*(uint8_t*)(kernel_base + 0x117C2) = 0xC3;

*(uint8_t*)(kernel_base + 0x13EF2F) = 0x31;
*(uint8_t*)(kernel_base + 0x13EF30) = 0xC0;
*(uint8_t*)(kernel_base + 0x13EF31) = 0x90;
*(uint8_t*)(kernel_base + 0x13EF32) = 0x90;
*(uint8_t*)(kernel_base + 0x13EF33) = 0x90;
```
Please make an pull request for anything that is missing or want to add something.

## Contributors
Massive thanks to the following:

- [qwertyoruiopz](https://twitter.com/qwertyoruiopz)
- [Flatz](https://twitter.com/flat_z)
- Anonymous

- [DarkElement](https://twitter.com/zordon605)
- [Vultra](https://twitter.com/C0rpVultra)
