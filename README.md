# x65

6502 Macro Assembler in a single c++ file using the struse single file text parsing library. Supports most syntaxes. x65 was recently named Asm6502 but was renamed because Asm6502 is too generic, x65 has no particular meaning.

![x65](bin/x65.png)

In order to minimize the documentation and make this page shorter I've moved the [old documentation](../../wiki/Previous-first-page) here.

The [up to date documentation is here](x65.txt).

x65 can assemble 6502, 65C02 and 65816 source and build executables for c64, Apple II or just raw binary.

Noteworthy features:

* Code with sections, object files and linking or single file fixed
  address, or mix it up with fixed address sections in object files.
* Assembler listing with cycle counting for code review.
* Export multiple binaries with a single link operation.
* C style scoping within '{' and '}' with local and pool labels
  respecting scopes.
* Conditional assembly with if/ifdef/else etc.
* Assembler directives representing a variety of features.
* Local labels can be defined in a number of ways, such as leading
  period (.label) or leading at-sign (@label) or terminating
  dollar sign (label$).
* String Symbols system allows building user expressions and macros
  during assembly.
* Reassignment of symbols and labels by default.
* No indentation required for instructions, meaning that labels can't
  be mnemonics, macros or directives.
* Supporting the syntax of other 6502 assemblers (Merlin syntax
  requires command line argument, -endm adds support for sources
  using macro/endmacro and repeat/endrepeat combos rather
  than scoeps).
* Apple II GS executable output.

## Features

* **Code**
* **Linking**
* **Comments**
* **Labels**
* **String Symbols**
* **Directives**
* **Macros**
* **Expressions**
* **List File with Cycle Count**

## Prerequisite

x65.cpp requires struse.h which is a single file text parsing library that can be retrieved from https://github.com/Sakrac/struse.

### References

* [6502 opcodes](http://www.6502.org/tutorials/6502opcodes.html)
* [6502 opcode grid](http://www.llx.com/~nparker/a2/opcodes.html)
* [Codebase64 CPU section](http://codebase64.org/doku.php?id=base:6502_6510_coding)
* [6502 illegal opcodes](http://www.oxyron.de/html/opcodes02.html)
* [65816 opcodes](http://wiki.superfamicom.org/snes/show/65816+Reference#fn:14)

### Download Binaries

* [Windows x64 binaries](../..//raw/master/bin/x65_x64.zip)
* [Windows x86 binaries](../..//raw/master/bin/x65_win32.zip)

### x65

x65 is the assembler

### x65macro.i

x65macro.i is a 6502 include file that defines a number of standard macros that can assign values, move values, copy values and loop constructs, see x65.txt for details.

### dump_x65

dump_x65 is a tool to inspect the contents of .x65 object files generated by x65 to track down linking issues

### x65dsasm

x65dsasm is a tool to disassemble assembled binary code for review, it will perform a basic analysis and assign labels where appropriate and treats unreferenced bytes as data rather than code. It can also export assemblable code from a binary.

### Acknowledgments

This project would not be completed without the direct or indirect support of great people, some which I can currently remember:

* Marc dePeo, helping me uncover the strange and unique world of Merlin's assembler syntax (and working together with me on True Crime NY gameplay code and more)
* Che Lalic, explaining the murky bits of 65816 (and a Ninja on SNES NBA Hangtime and other projects)
* John Brooks, sharing the Rastan Apple II source code so I could test 65816 and figure out a number of issues with my initial linker, and encouraging the implementation of Apple II GS OS executable file format / OMF export (and helping out with Playstation All-Stars)
* [Brutal Deluxe](http://www.brutaldeluxe.fr) for releasing the excellent OMF Analyzer tool and the source, which was a significant help generating Apple II GS OS executables.
* The C64 demo scene for sharing a great deal of 6502 programming resources and overall inspiration.
* Jordan Mechner, sharing the Prince of Persia Apple II source code so I could test out a significant part of the assembler and the Merlin syntax mode
* Bill Budge, sharing the Pinball Construction Set Apple II source code, although at the point I tried it, all of it just assembled without any assembler issues at all.

### Development Status

Looking for help testing various features of the assembler, I have a large number of tests that pass without fail but there are so many ways for assemblers to break.
Primarily tested with personal archive of sources written for Kick assmebler, DASM, TASM, XASM, etc. and passing most of Apple II Prince of Persia and Pinball Construction set.

**TODO**
* irp (indefinite repeat)

**FIXED**
* Adding x65macro.i
* Vice symbols will generate breakpoints whenever label 'debugbreak' is encountered
* Evaluating '==' was broken
* Macros can have dots in their names
* Handling double negative in expressions (--35 == 35)
* Macros works within conditionals (if/else/endif, etc)
* String symbols broke late evaluation resulting in garbage references, this has been fixed
* Added string symbols
* Resolved the DirectPage_Stack section vs. Zeropage section for Apple II GS/OS executables.
* OMF export for Apple II GS/OS executables

[(older fixes)](../../wiki/fixes)

Revisions:
* 10 - String Symbols
* 9 - Apple II GS OS executable
* 8 - Fish food / Linking tested and passed with external project (Apple II gs Rastan)
* 7 - 65816 Support
* 6 - 65C02 support
* 5 - Merlin syntax
* 4 - Object files, relative sections and linking
* 3 - 6502 full support
* 2 - Moved file out of struse samples
* 1 - Built a sample of a simple assembler within struse
