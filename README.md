# XenonRecomp Compiled Files for Linux
* Using Windows 10 X86_64 (WLS2 with Debian 12)
* GNU Make 4.3 Built for x86_64-pc-linux-gnu
* cmake version 3.25.1
  
# Troubleshooting
These compiled files were made possible after addressing some bugs in the implementation of some headers in the code.<br>
Particularly in the <b>xbox.h</b> and <b>xdbf.h</b> files.
<h3>xbox.h</h3>
Patch blocks 243 to 263 to fix issues with unions:
<code>
typedef struct _XXOVERLAPPED {
    union 
    {
        struct
        {
            be<uint32_t> Error;
            be<uint32_t> Length;
        } errorLength;

        struct
        {
            uint32_t InternalLow;
            uint32_t InternalHigh;
        } internalParts;
    }data;
    uint32_t InternalContext;
    be<uint32_t> hEvent;
    be<uint32_t> pCompletionRoutine;
    be<uint32_t> dwCompletionContext;
    be<uint32_t> dwExtendedError;
} XXOVERLAPPED, *PXXOVERLAPPED;
</code>

<h3>xdbf.h</h3>
Patch block 129 to 138 to remove anonymity:
<code>
union XDBFTitleID
{
    struct
    {
        be<uint16_t> u16;
        char u8[0x02];
    }parts;
    be<uint32_t> u32;
};
</code>
 
# Thanks
Base on <a href="https://github.com/hedge-dev/XenonRecomp">Edge-dev</a> project. 
