typedef unsigned long long u64;
typedef unsigned int u32;
typedef unsigned short u16;
typedef unsigned char u8;

typedef u64 EFI_STATUS;
typedef void* EFI_HANDLE;
typedef void* EFI_EVENT;

#define EFIAPI

struct EFI_SYSTEM_TABLE;
struct EFI_BOOT_SERVICES;
struct EFI_RUNTIME_SERVICES;
struct EFI_SIMPLE_TEXT_INPUT_PROTOCOL;
struct EFI_SIMPLE_TEXT_OUTPUT_PROTOCOL;
struct EFI_INPUT_KEY;

typedef struct {
    u64 Signature;
    u32 Revision;
    u32 HeaderSize;
    u32 CRC32;
    u32 Reserved;
} EFI_TABLE_HEADER;

typedef struct EFI_INPUT_KEY {
    u16 ScanCode;
    u16 UnicodeChar;
} EFI_INPUT_KEY;

typedef struct EFI_SIMPLE_TEXT_INPUT_PROTOCOL {
    EFI_STATUS (*Reset)(struct EFI_SIMPLE_TEXT_INPUT_PROTOCOL* This, u8 ExtendedVerification);
    EFI_STATUS (*ReadKeyStroke)(struct EFI_SIMPLE_TEXT_INPUT_PROTOCOL* This, EFI_INPUT_KEY* Key);
    EFI_EVENT WaitForKey;
} EFI_SIMPLE_TEXT_INPUT_PROTOCOL;

typedef struct EFI_SIMPLE_TEXT_OUTPUT_PROTOCOL {
    u64 _buf[10];
    EFI_STATUS (*OutputString)(struct EFI_SIMPLE_TEXT_OUTPUT_PROTOCOL* This, u16* String);
    u64 _buf2[4];
    EFI_STATUS (*ClearScreen)(struct EFI_SIMPLE_TEXT_OUTPUT_PROTOCOL* This);
} EFI_SIMPLE_TEXT_OUTPUT_PROTOCOL;

typedef struct EFI_BOOT_SERVICES {
    EFI_TABLE_HEADER Hdr;
    void* RaiseTPL;
    void* RestoreTPL;
    void* AllocatePages;
    void* FreePages;
    void* GetMemoryMap;
    void* AllocatePool;
    void* FreePool;
    void* CreateEvent;
    void* SetTimer;
    EFI_STATUS (*WaitForEvent)(u64 NumberOfEvents, EFI_EVENT* Event, u64* Index);
    void* SignalEvent;
    void* CloseEvent;
    void* CheckEvent;
    void* InstallProtocolInterface;
    void* ReinstallProtocolInterface;
    void* UninstallProtocolInterface;
    void* HandleProtocol;
    void* RegisterProtocolNotify;
    void* LocateHandle;
    void* LocateDevicePath;
    void* InstallConfigurationTable;
    void* LoadImage;
    void* StartImage;
    void* Exit;
    void* UnloadImage;
    void* ExitBootServices;
    void* GetNextMonotonicCount;
    void* Stall;
    void* SetWatchdogTimer;
    void* ConnectController;
    void* DisconnectController;
    void* OpenProtocol;
    void* CloseProtocol;
    void* OpenProtocolInformation;
    void* ProtocolsPerHandle;
    void* LocateHandleBuffer;
    void* LocateProtocol;
    void* InstallMultipleProtocolInterfaces;
    void* UninstallMultipleProtocolInterfaces;
    void* CalculateCrc32;
    void* CopyMem;
    void* SetMem;
    void* CreateEventEx;
} EFI_BOOT_SERVICES;

typedef struct EFI_RUNTIME_SERVICES {
    EFI_TABLE_HEADER Hdr;
    void* GetTime;
    void* SetTime;
    void* GetWakeupTime;
    void* SetWakeupTime;
    void* SetVirtualAddressMap;
    void* ConvertPointer;
    void* GetVariable;
    void* GetNextVariableName;
    void* SetVariable;
    void* GetNextHighMonotonicCount;
    void (*ResetSystem)(u64 ResetType, EFI_STATUS ResetStatus, u64 DataSize, void* ResetData);
} EFI_RUNTIME_SERVICES;

typedef struct EFI_SYSTEM_TABLE {
    EFI_TABLE_HEADER Hdr;
    u16* FirmwareVendor;
    u32 FirmwareRevision;
    EFI_HANDLE ConsoleInHandle;
    EFI_SIMPLE_TEXT_INPUT_PROTOCOL* ConIn;
    EFI_HANDLE ConsoleOutHandle;
    EFI_SIMPLE_TEXT_OUTPUT_PROTOCOL* ConOut;
    EFI_HANDLE StandardErrorHandle;
    EFI_SIMPLE_TEXT_OUTPUT_PROTOCOL* StdErr;
    EFI_RUNTIME_SERVICES* RuntimeServices;
    EFI_BOOT_SERVICES* BootServices;
    u64 NumberOfTableEntries;
    void* ConfigurationTable;
} EFI_SYSTEM_TABLE;

#define EFI_SUCCESS 0

static EFI_SYSTEM_TABLE* gST;

static int cx;
static int cy;

static char* vga;

static EFI_SIMPLE_TEXT_INPUT_PROTOCOL* conin;

static int len(const char* s) {
    int n = 0;

    if(!s)
        return 0;

    while(s[n])
        n = n + 1;

    return n;
}

static void cpy(char* d, const char* s) {
    if(!d || !s)
        return;

    while((*d = *s)) {
        d = d + 1;
        s = s + 1;
    }
}

static void cat(char* d, const char* s) {
    if(!d || !s)
        return;

    while(*d)
        d = d + 1;

    while((*d = *s)) {
        d = d + 1;
        s = s + 1;
    }
}

static int cmp(const char* a, const char* b) {
    if(!a || !b)
        return -1;

    while(*a && *a == *b) {
        a = a + 1;
        b = b + 1;
    }

    return (unsigned char)*a - (unsigned char)*b;
}

static int ncmp(const char* a, const char* b, int n) {
    int i;

    if(!a || !b)
        return -1;

    for(i = 0; i < n; i = i + 1) {
        if(a[i] != b[i])
            return (unsigned char)a[i] - (unsigned char)b[i];

        if(a[i] == 0)
            break;
    }

    return 0;
}

static int casecmp(const char* a, const char* b) {
    char ca;
    char cb;

    if(!a || !b)
        return -1;

    while(*a && *b) {

        ca = (*a >= 'A' && *a <= 'Z')
            ? *a + 32
            : *a;

        cb = (*b >= 'A' && *b <= 'Z')
            ? *b + 32
            : *b;

        if(ca != cb)
            return ca - cb;

        a = a + 1;
        b = b + 1;
    }

    return (*a ? 1 : (*b ? -1 : 0));
}

static char* chrs(const char* s, int c) {
    if(!s)
        return 0;

    while(*s && *s != (char)c)
        s = s + 1;

    return (*s == (char)c)
        ? (char*)s
        : 0;
}

static void zero(void* ptr, int size) {
    unsigned char* p;
    int i;

    p = (unsigned char*)ptr;

    for(i = 0; i < size; i = i + 1)
        p[i] = 0;
}

static u64 toint(const char* s) {
    u64 res;
    int sign;

    if(!s)
        return 0;

    res = 0;
    sign = 1;

    if(*s == '-') {
        sign = -1;
        s = s + 1;
    }

    while(*s >= '0' && *s <= '9') {
        res = res * 10 + (*s - '0');
        s = s + 1;
    }

    if(sign < 0)
        return (u64)(-(long long)res);

    return res;
}

void putc(char c) {
    u16 buf[2];

    buf[0] = (u16)c;
    buf[1] = 0;

    if(vga) {

        EFI_SIMPLE_TEXT_OUTPUT_PROTOCOL* con;

        con = (EFI_SIMPLE_TEXT_OUTPUT_PROTOCOL*)vga;

        if(c == '\n') {

            u16 newline[] = {
                '\r',
                '\n',
                0
            };

            con->OutputString(con, newline);
        }
        else {
            con->OutputString(con, buf);
        }
    }
}

void print(const char* s) {
    if(!s)
        return;

    while(*s) {
        putc(*s);
        s = s + 1;
    }
}

void print_hex(u64 n) {
    const char hex[] = "0123456789ABCDEF";

    char buf[17];

    int i;

    for(i = 0; i < 17; i = i + 1)
        buf[i] = 0;

    i = 16;

    do {
        i = i - 1;

        buf[i] = hex[n & 0xF];

        n = n >> 4;

    } while(n > 0 && i > 0);

    print(&buf[i]);
}

void print_dec(u64 n) {
    char buf[21];

    int i;

    for(i = 0; i < 21; i = i + 1)
        buf[i] = 0;

    i = 20;

    do {
        i = i - 1;

        buf[i] = '0' + (n % 10);

        n = n / 10;

    } while(n > 0);

    print(&buf[i]);
}

void cls(void) {
    if(vga) {
        ((EFI_SIMPLE_TEXT_OUTPUT_PROTOCOL*)vga)->ClearScreen(
            (EFI_SIMPLE_TEXT_OUTPUT_PROTOCOL*)vga
        );
    }

    cx = 0;
    cy = 0;
}

char getkey(void) {
    EFI_INPUT_KEY key;

    EFI_STATUS status;

    u64 idx;

    if(!conin)
        return 0;

    while(1) {

        gST->BootServices->WaitForEvent(
            1,
            &conin->WaitForKey,
            &idx
        );

        status = conin->ReadKeyStroke(
            conin,
            &key
        );

        if(status == EFI_SUCCESS) {

            if(key.UnicodeChar >= 0x20 &&
               key.UnicodeChar <= 0x7E) {

                return (char)key.UnicodeChar;
            }

            if(key.UnicodeChar == 0x0D)
                return '\n';

            if(key.UnicodeChar == 0x08)
                return '\b';
        }
    }
}

void readline(char* buf, int size) {
    int p;
    char c;

    p = 0;

    while(1) {

        c = getkey();

        if(c == '\n') {
            print("\n");
            break;
        }

        if(c == '\b' && p > 0) {
            p = p - 1;
        }

        else if(p < size - 1 &&
                c >= 32 &&
                c <= 126) {

            buf[p] = c;

            p = p + 1;

            putc(c);
        }
    }

    buf[p] = 0;
}

void reboot(void) {
    print("\nREBOOTING...\n");

    if(gST &&
       gST->RuntimeServices &&
       gST->RuntimeServices->ResetSystem) {

        gST->RuntimeServices->ResetSystem(
            0,
            0,
            0,
            0
        );
    }

    while(1);
}

typedef struct {
    u64 qword;
} Reg;

typedef struct {
    Reg regs[16];
    Reg stack[4096];

    long long sp;

    int zf;
    int cf;
    int of;
    int sf;
} VM;

static VM cpu;

static long long vars[26];

static char tvars[26][256];

static char scripts[1024][2048];

static char asm_storage[1024][2048];

static long long z;
static int regidx(const char* n) {
    if(!n) return -1;

    if(casecmp(n,"rax")==0||casecmp(n,"eax")==0||casecmp(n,"ax")==0||casecmp(n,"al")==0||casecmp(n,"ah")==0) return 0;
    if(casecmp(n,"rcx")==0||casecmp(n,"ecx")==0||casecmp(n,"cx")==0||casecmp(n,"cl")==0||casecmp(n,"ch")==0) return 1;
    if(casecmp(n,"rdx")==0||casecmp(n,"edx")==0||casecmp(n,"dx")==0||casecmp(n,"dl")==0||casecmp(n,"dh")==0) return 2;
    if(casecmp(n,"rbx")==0||casecmp(n,"ebx")==0||casecmp(n,"bx")==0||casecmp(n,"bl")==0||casecmp(n,"bh")==0) return 3;
    if(casecmp(n,"rsp")==0||casecmp(n,"esp")==0||casecmp(n,"sp")==0) return 4;
    if(casecmp(n,"rbp")==0||casecmp(n,"ebp")==0||casecmp(n,"bp")==0) return 5;
    if(casecmp(n,"rsi")==0||casecmp(n,"esi")==0||casecmp(n,"si")==0) return 6;
    if(casecmp(n,"rdi")==0||casecmp(n,"edi")==0||casecmp(n,"di")==0) return 7;
    if(casecmp(n,"r8")==0) return 8;
    if(casecmp(n,"r9")==0) return 9;
    if(casecmp(n,"r10")==0) return 10;
    if(casecmp(n,"r11")==0) return 11;
    if(casecmp(n,"r12")==0) return 12;
    if(casecmp(n,"r13")==0) return 13;
    if(casecmp(n,"r14")==0) return 14;
    if(casecmp(n,"r15")==0) return 15;

    return -1;
}

static u64 regval(int i, const char* n) {

    if(casecmp(n,"ah")==0||
       casecmp(n,"bh")==0||
       casecmp(n,"ch")==0||
       casecmp(n,"dh")==0)

        return (cpu.regs[i].qword >> 8) & 0xFF;

    if(len(n)==2 &&
      (n[1]=='l'||n[1]=='L'))

        return cpu.regs[i].qword & 0xFF;

    if(len(n)==2 &&
      (n[1]=='x'||n[1]=='X'))

        return cpu.regs[i].qword & 0xFFFF;

    if(len(n)==3 &&
      (n[0]=='e'||n[0]=='E'))

        return cpu.regs[i].qword & 0xFFFFFFFFULL;

    return cpu.regs[i].qword;
}

static void setreg(int i, const char* n, u64 v) {

    if(casecmp(n,"ah")==0||
       casecmp(n,"bh")==0||
       casecmp(n,"ch")==0||
       casecmp(n,"dh")==0)

        cpu.regs[i].qword =
            (cpu.regs[i].qword & 0xFFFFFFFFFFFF00FFULL) |
            ((v & 0xFF) << 8);

    else if(len(n)==2 &&
           (n[1]=='l'||n[1]=='L'))

        cpu.regs[i].qword =
            (cpu.regs[i].qword & 0xFFFFFFFFFFFFFF00ULL) |
            (v & 0xFF);

    else if(len(n)==2 &&
           (n[1]=='x'||n[1]=='X'))

        cpu.regs[i].qword =
            (cpu.regs[i].qword & 0xFFFFFFFFFFFF0000ULL) |
            (v & 0xFFFF);

    else if(len(n)==3 &&
           (n[0]=='e'||n[0]=='E'))

        cpu.regs[i].qword = (u32)v;

    else
        cpu.regs[i].qword = v;
}

static void push(u64 v) {

    if(cpu.sp >= 4094) {
        print("STACK_OVERFLOW\n");
        reboot();
    }

    cpu.sp = cpu.sp + 1;

    cpu.stack[cpu.sp].qword = v;

    print("  [STACK] PUSH 0x");
    print_hex(v);
    print("\n");
}

static u64 pop(void) {
    u64 v;

    if(cpu.sp < 0) {
        print("STACK_UNDERFLOW\n");
        reboot();
    }

    v = cpu.stack[cpu.sp].qword;

    cpu.sp = cpu.sp - 1;

    print("  [STACK] POP 0x");
    print_hex(v);
    print("\n");

    return v;
}

void run_asm(int id) {

    char line[2048];

    char* ptr;

    char cmd[32];

    int i;

    int idx;

    int sidx;

    u64 a;
    u64 b;
    u64 res;

    char dest[16];

    char src[32];

    if(id < 0 || id >= 1024) {
        print("ASM_SLOT_OUT_OF_BOUNDS\n");
        reboot();
    }

    if(asm_storage[id][0] == 0) {

        print("[ASM-");
        print_dec(id);
        print("] Empty\n");

        return;
    }

    zero(&cpu.regs, sizeof(cpu.regs));

    cpu.sp = -1;

    cpu.zf = 0;
    cpu.cf = 0;
    cpu.of = 0;
    cpu.sf = 0;

    cpu.regs[0].qword = vars[0];

    print("\n[ASM-");
    print_dec(id);
    print("] Executing: ");
    print(asm_storage[id]);

    print("\n----------------------------------------\n");

    cpy(line, asm_storage[id]);

    ptr = line;

    while(*ptr) {

        while(*ptr==' '||
              *ptr=='\n'||
              *ptr=='\t')

            ptr = ptr + 1;

        if(!*ptr)
            break;

        i = 0;

        while(*ptr &&
             *ptr!=' ' &&
             *ptr!='\n' &&
             *ptr!='\t' &&
             i<31) {

            cmd[i] = *ptr;

            i = i + 1;

            ptr = ptr + 1;
        }

        cmd[i] = 0;

        if(casecmp(cmd,"mov")==0) {

            while(*ptr==' '||*ptr=='\t')
                ptr = ptr + 1;

            i = 0;

            while(*ptr &&
                 *ptr!=' ' &&
                 *ptr!='\t' &&
                 *ptr!=',' &&
                 i<15) {

                dest[i] = *ptr;

                i = i + 1;

                ptr = ptr + 1;
            }

            dest[i] = 0;

            while(*ptr==' '||
                 *ptr=='\t'||
                 *ptr==',')

                ptr = ptr + 1;

            i = 0;

            while(*ptr &&
                 *ptr!=' ' &&
                 *ptr!='\n' &&
                 *ptr!='\t' &&
                 i<31) {

                src[i] = *ptr;

                i = i + 1;

                ptr = ptr + 1;
            }

            src[i] = 0;

            idx = regidx(dest);

            if(idx < 0) {

                if(dest[0]>='a' &&
                   dest[0]<='z') {

                    if((src[0]>='0'&&src[0]<='9') ||
                       (src[0]=='-'&&src[1]>='0'&&src[1]<='9'))

                        vars[dest[0]-'a'] =
                            (long long)toint(src);

                    else {

                        sidx = regidx(src);

                        if(sidx>=0)
                            vars[dest[0]-'a'] =
                                (long long)regval(sidx, src);
                    }
                }
            }
            else {

                if((src[0]>='0'&&src[0]<='9') ||
                   (src[0]=='-'&&src[1]>='0'&&src[1]<='9'))

                    setreg(idx, dest, toint(src));

                else {

                    sidx = regidx(src);

                    if(sidx>=0)
                        setreg(idx, dest,
                               regval(sidx, src));
                }
            }

            print("  mov ");
            print(dest);
            print(", ");
            print(src);
            print("\n");
        }

        else if(casecmp(cmd,"push")==0) {

            while(*ptr==' '||*ptr=='\t')
                ptr = ptr + 1;

            i = 0;

            while(*ptr &&
                 *ptr!=' ' &&
                 *ptr!='\n' &&
                 *ptr!='\t' &&
                 i<31) {

                src[i] = *ptr;

                i = i + 1;

                ptr = ptr + 1;
            }

            src[i] = 0;

            idx = regidx(src);

            if(idx>=0)
                push(regval(idx, src));

            else if((src[0]>='0'&&src[0]<='9') ||
                    (src[0]=='-'&&src[1]>='0'&&src[1]<='9'))

                push(toint(src));

            else if(src[0]>='a'&&src[0]<='z')

                push((u64)vars[src[0]-'a']);
        }

        else if(casecmp(cmd,"pop")==0) {

            while(*ptr==' '||*ptr=='\t')
                ptr = ptr + 1;

            i = 0;

            while(*ptr &&
                 *ptr!=' ' &&
                 *ptr!='\n' &&
                 *ptr!='\t' &&
                 i<15) {

                dest[i] = *ptr;

                i = i + 1;

                ptr = ptr + 1;
            }

            dest[i] = 0;

            res = pop();

            idx = regidx(dest);

            if(idx>=0)
                setreg(idx, dest, res);

            else if(dest[0]>='a'&&dest[0]<='z')
                vars[dest[0]-'a'] = (long long)res;

            print("  pop ");
            print(dest);
            print(" = 0x");
            print_hex(res);
            print("\n");
        }
        else if(casecmp(cmd,"add")==0 ||
                casecmp(cmd,"sub")==0) {

            int is_sub;

            is_sub = (casecmp(cmd,"sub")==0);

            while(*ptr==' '||*ptr=='\t')
                ptr = ptr + 1;

            i = 0;

            while(*ptr &&
                 *ptr!=' ' &&
                 *ptr!='\t' &&
                 *ptr!=',' &&
                 i<15) {

                dest[i] = *ptr;

                i = i + 1;

                ptr = ptr + 1;
            }

            dest[i] = 0;

            while(*ptr==' '||
                 *ptr=='\t'||
                 *ptr==',')

                ptr = ptr + 1;

            i = 0;

            while(*ptr &&
                 *ptr!=' ' &&
                 *ptr!='\n' &&
                 *ptr!='\t' &&
                 i<31) {

                src[i] = *ptr;

                i = i + 1;

                ptr = ptr + 1;
            }

            src[i] = 0;

            idx = regidx(dest);

            if(idx < 0) {
                print("ADD/SUB invalid register\n");
                reboot();
            }

            a = regval(idx, dest);

            if((src[0]>='0'&&src[0]<='9') ||
               (src[0]=='-'&&src[1]>='0'&&src[1]<='9'))

                b = toint(src);

            else {

                sidx = regidx(src);

                if(sidx>=0)
                    b = regval(sidx, src);
                else
                    b = 0;
            }

            if(is_sub)
                res = a - b;
            else
                res = a + b;

            setreg(idx, dest, res);

            cpu.zf = (res == 0);

            print("  ");
            print(is_sub ? "sub" : "add");
            print(" ");
            print(dest);
            print(", ");
            print(src);
            print(" = 0x");
            print_hex(res);
            print("\n");
        }

        else if(casecmp(cmd,"mul")==0) {

            while(*ptr==' '||*ptr=='\t')
                ptr = ptr + 1;

            i = 0;

            while(*ptr &&
                 *ptr!=' ' &&
                 *ptr!='\n' &&
                 *ptr!='\t' &&
                 i<31) {

                src[i] = *ptr;

                i = i + 1;

                ptr = ptr + 1;
            }

            src[i] = 0;

            sidx = regidx(src);

            if(sidx < 0) {
                print("MUL invalid register\n");
                reboot();
            }

            res = cpu.regs[0].qword *
                  regval(sidx, src);

            cpu.regs[0].qword = res;

            cpu.zf = (res == 0);

            print("  mul ");
            print(src);
            print(" = 0x");
            print_hex(res);
            print("\n");
        }

        else if(casecmp(cmd,"uppercase_loop")==0) {

            int idx2;

            idx2 = 0;

            while(tvars[0][idx2]) {

                if(tvars[0][idx2]>='a' &&
                   tvars[0][idx2]<='z')

                    tvars[0][idx2] =
                        tvars[0][idx2] - 32;

                idx2 = idx2 + 1;
            }

            print("  uppercase_loop: '");
            print(tvars[0]);
            print("'\n");
        }

        while(*ptr && *ptr!='\n')
            ptr = ptr + 1;

        if(*ptr=='\n')
            ptr = ptr + 1;
    }

    z = (long long)cpu.regs[0].qword;

    vars[0] = z;

    print("[ASM-");
    print_dec(id);
    print("] Done. Z=");
    print_dec((u64)z);
    print(" | SP=");
    print_dec((u64)cpu.sp);
    print("\n\n");
}

void exec_cmd(char* c) {

    int id;

    char* sp;

    char tmp[2048];

    char* l;

    char* next;

    char save;

    int i;

    if(len(c) < 1)
        return;

    if(cmp(c,"typo-opc")==0) {

        print("=== TypoOS Commands ===\n");
        print("  typo-set-X value\n");
        print("  typo-read-X\n");
        print("  typo-tset-X text\n");
        print("  typo-tread-X\n");
        print("  typo-script-ID\n");
        print("  typo-start-ID\n");
        print("  typo-list\n");
        print("  typo-stack\n");
        print("  typo-regs\n");
        print("  typo-cls\n");
        print("  typo-crash\n");
        print("  asm-ID\n");
        print("  exit\n");
    }

    else if(cmp(c,"typo-stack")==0) {

        print("=== STACK DUMP ===\n");

        if(cpu.sp < 0)
            print("  Stack is empty\n");

        else {

            print("  SP = ");
            print_dec((u64)cpu.sp);
            print(" (top)\n");

            for(i = cpu.sp;
                i >= 0 && i >= cpu.sp - 15;
                i = i - 1) {

                print("  [");
                print_dec((u64)i);
                print("] = 0x");

                print_hex(cpu.stack[i].qword);

                print(" (");

                print_dec(cpu.stack[i].qword);

                print(")\n");
            }

            if(cpu.sp > 15) {

                print("  ... and ");

                print_dec((u64)(cpu.sp - 15));

                print(" more\n");
            }
        }
    }

    else if(ncmp(c,"typo-asm-",9)==0) {

        id = (int)toint(c + 9);

        print("[ASM EDIT ");

        print_dec((u64)id);

        print("] Type 'end' on new line to save.\n");

        asm_storage[id][0] = 0;

        while(1) {

            char line[256];

            print("asm");

            print_dec((u64)id);

            print("> ");

            readline(line, 256);

            if(cmp(line,"end")==0)
                break;

            cat(asm_storage[id], line);

            cat(asm_storage[id], "\n");
        }

        print("ASM [");

        print_dec((u64)id);

        print("] saved (");

        print_dec((u64)len(asm_storage[id]));

        print(" bytes)\n");
    }

    else if(cmp(c,"typo-regs")==0) {

        print("=== REGISTERS ===\n");

        print("RAX=");
        print_hex(cpu.regs[0].qword);
        print("\n");

        print("RBX=");
        print_hex(cpu.regs[3].qword);
        print("\n");

        print("RCX=");
        print_hex(cpu.regs[1].qword);
        print("\n");

        print("RDX=");
        print_hex(cpu.regs[2].qword);
        print("\n");
    }
    else if(cmp(c,"typo-list")==0) {

        int ct;

        ct = 0;

        print("=== TypoOS TASK MANAGER ===\n");

        for(i = 0; i < 1024; i = i + 1) {

            if(len(scripts[i]) > 0) {

                print("Script [");

                print_dec((u64)i);

                print("]: ");

                print_dec((u64)len(scripts[i]));

                print(" bytes\n");

                ct = ct + 1;
            }
        }

        for(i = 0; i < 1024; i = i + 1) {

            if(len(asm_storage[i]) > 0) {

                print("ASM [");

                print_dec((u64)i);

                print("]: ");

                print(asm_storage[i]);

                ct = ct + 1;
            }
        }

        if(ct == 0)
            print("RAM is empty.\n");
    }

    else if(cmp(c,"typo-cls")==0) {

        cls();
    }

    else if(cmp(c,"typo-crash")==0) {

        reboot();
    }

    else if(ncmp(c,"typo-set-",9)==0) {

        vars[c[9]-'a'] =
            (long long)toint(c + 10);

        print("var_");

        putc(c[9]);

        print(" = ");

        print_dec(
            (u64)vars[c[9]-'a']
        );

        print("\n");
    }

    else if(ncmp(c,"typo-read-",10)==0) {

        if(c[10]=='z') {

            print_dec((u64)z);

            print("\n");
        }

        else {

            print_dec(
                (u64)vars[c[10]-'a']
            );

            print("\n");
        }
    }

    else if(ncmp(c,"typo-tset-",10)==0) {

        sp = chrs(c, ' ');

        if(sp) {

            cpy(
                tvars[c[10]-'a'],
                sp + 1
            );

            print("text_");

            putc(c[10]);

            print(" = '");

            print(tvars[c[10]-'a']);

            print("'\n");
        }
    }

    else if(ncmp(c,"typo-tread-",11)==0) {

        print(tvars[c[11]-'a']);

        print("\n");
    }

    else if(ncmp(c,"typo-script-",12)==0) {

        id = (int)toint(c + 12);

        print("[EDIT ");

        print_dec((u64)id);

        print("] Type 'end' on new line to save.\n");

        scripts[id][0] = 0;

        while(1) {

            char line[256];

            print_dec((u64)id);

            print("> ");

            readline(line, 256);

            if(cmp(line,"end")==0)
                break;

            cat(scripts[id], line);

            cat(scripts[id], "\n");
        }

        print("Script [");

        print_dec((u64)id);

        print("] saved (");

        print_dec(
            (u64)len(scripts[id])
        );

        print(" bytes)\n");
    }

    else if(ncmp(c,"typo-start-",11)==0) {

        id = (int)toint(c + 11);

        cpy(tmp, scripts[id]);

        l = tmp;

        while(*l) {

            next = l;

            while(*next &&
                 *next != '\n')

                next = next + 1;

            save = *next;

            *next = 0;

            exec_cmd(l);

            *next = save;

            if(save)
                l = next + 1;
            else
                l = next;
        }
    }

    else if(ncmp(c,"asm-",4)==0) {

        run_asm(
            (int)toint(c + 4)
        );
    }

    else if(len(c) > 0 &&
           c[0] != '#') {

        print("Unknown command: ");

        print(c);

        print("\n");
    }
}

EFI_STATUS EFIAPI efi_main(
    EFI_HANDLE ImageHandle,
    EFI_SYSTEM_TABLE* SystemTable
) {

    char in[256];

    gST = SystemTable;

    vga = (char*)SystemTable->ConOut;

    conin = SystemTable->ConIn;

    cls();

    cpy(
        asm_storage[0],
        "mov al, 255\n"
        "push al\n"
        "pop bl\n"
    );

    cpy(
        asm_storage[1],
        "mov ax, 65535\n"
        "push ax\n"
        "pop cx\n"
    );

    cpy(
        asm_storage[2],
        "mov eax, 4294967295\n"
        "push eax\n"
        "pop edx\n"
    );

    cpy(
        asm_storage[3],
        "mov rax, 18446744073709551615\n"
        "push rax\n"
        "pop rbx\n"
    );

    cpy(
        asm_storage[4],
        "push 10\n"
        "push 20\n"
        "push 30\n"
        "pop rax\n"
        "pop rbx\n"
        "pop rcx\n"
        "add rax, rbx\n"
    );

    cpy(
        asm_storage[5],
        "uppercase_loop\n"
    );

    print("TypoOS 2.0.0 - UEFI Edition\n");

    print("Type 'typo-opc' for commands\n\n");

    while(1) {

        print("typoos$ ");

        readline(in, 256);

        if(cmp(in,"exit")==0)
            break;

        exec_cmd(in);
    }

    if(SystemTable->RuntimeServices &&
       SystemTable->RuntimeServices->ResetSystem) {

        SystemTable
            ->RuntimeServices
            ->ResetSystem(
                0,
                0,
                0,
                0
            );
    }

    return EFI_SUCCESS;
}
