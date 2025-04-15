# XenonRecomp Compiled Files for Linux
* Using Windows 10 X86_64 (WLS2 with Debian 12)
* GNU Make 4.3 Built for x86_64-pc-linux-gnu
* cmake version 3.25.1
* git version 2.39.5

# How to use
* Open a linux shell or terminal
* Clone repository with: <code>git clone [https://github.com/aayes89/XenonRecompCompiledFiles.git](https://github.com/aayes89/XenonRecompCompiledFiles.git)</code>
* Give executable permissions with: <code>chmod u+x XenonRecomp XenonAnalyse XenosRecomp xxhsum</code>
* Enjoy

# Usages:
- XenonAnalyse:
	-  XenonAnalyse [input XEX file path] [output jump table TOML file path]
- XenonRecomp:
	-  XenonRecomp [input TOML file path] [PPC context header file path]
- XenosRecomp:
	-  XenosRecomp [input path] [output path] [shader common header file path]

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
        
<h3>shader_recompiler.cpp</h3>
Patch on structs:
<code>
    struct{
        uint32_t code1;
        uint32_t code2;
        uint32_t code3;
        uint32_t code4;
    };
    struct{
        int8_t x;
	    int8_t y;
	    int8_t z;
	    int8_t w;
    };
</code>
to
<code>
    struct Code_flow{
        uint32_t code1;
        uint32_t code2;
        uint32_t code3;
        uint32_t code4;
    };
    Code_flow cf;
    struct VarInt8{
        int8_t x;
	    int8_t y;
	    int8_t z;
	    int8_t w;
    };
    VarInt8 vint;
</code>

 
# Thanks
Base on <a href="https://github.com/hedge-dev/XenonRecomp">Edge-dev</a> project. 
