# GSoC 2023 Project Report | GCC

## Bypass assembler when generating LTO object files
**Contributor**: [Rishi Raj ](https://github.com/rsh-raj) </br>
**Mentors**: [ Jan Hubička](https://www.linkedin.com/in/jan-hubi%C4%8Dka-a9083984/?originalSubdomain=cz), [Martin Jambor](https://www.linkedin.com/in/martinjambor/?originalSubdomain=cz) </br>

**Project Size** : Medium (~175 hours) </br>
**Project repo**: [patch-submission](https://github.com/rsh-raj/gcc/tree/patch-submission)</br>
**Project Proposal**: [Proposal](https://docs.google.com/document/d/1r9kzsU96kOYfIhWZx62jx4ALG-J_aJs5U0sDpwFUtts/edit?usp=sharing)
## Project abstract
Link Time Optimization (LTO) enables GCC to dump its internal representation (GIMPLE) to disk so that a single executable can be optimized as a single module. The current implementation creates an assembly file, and the assembler is used to create the final LTO object file. This project aims to create Link-time-optimization (LTO) object files directly from the compiler to improve compile time performance significantly by bypassing the assembler. The GCC's LTO infrastructure has matured enough to compile large real-world applications. Thus, this project will significantly reduce their compile time once completed. 
## Project Goals
- Teach Libiberty's simple object to output .symtab and relocation sections in the object file.
- Extend dwarf2out.cc to output debug sections and symbol to object file bypassing the asm.
- Start with ELF and X86-64 support, and add the rest of the object file formats and architectures later on.
## Project Results
### Extending the libiberty simple object
In order to bypass the assembler, we needed support from libiberty to output the debug info section and their relocations directly to the object file, but it was missing. I spent the first half of summers extending the capabilities of libiberty. It was fun to learn about different object file formats (ELF, COFF, Mach, etc) and debugging in bits (quite literally!). I've also learned a lot from studying existing code, like structuring it, writing it clearly, and using the right comments.
### Extending dwarf2out.cc to bypass assembler
This was the most involved and somewhat tricky part. The main problem was my unfamiliarity with the DWARF debug format, lack of documentation on GCC dwarf implementation and relocations. With some digging around, guidance from my mentors, and Richard's help, I successfully navigated through this stage. I have successfully extended dwarf2out.c to output debug sections and their relocations directly to the object file.



# Contributions

|Commit/PR|Descritption|
|---|---|
[Commit: b13c068](https://github.com/gcc-mirror/gcc/commit/b13c0682ab290166a4a4c25513fec96beab5e211) | Applied Honza's previous patch on current sources ||
[Commit: 48ef456](https://github.com/gcc-mirror/gcc/commit/48ef456a8ec8b6df2f6e097a55872921b9f9b08c) | Added `.symtab` support||
[Commit: 31ff5e2](https://github.com/gcc-mirror/gcc/commit/31ff5e249df46ff122b115c86af04022307fafa4) | fixed header file dependency error during bootstrapped build||
[Commit: 6c3f792](https://github.com/gcc-mirror/gcc/commit/6c3f792ed56e99feb816bcd2caf16d1ef092ce00)| Extended libiberty to output X86_64 relocations
[Commit: 4e4c187](https://github.com/gcc-mirror/gcc/commit/4e4c18709986228750e0ca8e1cb48c4e6b38212a) | Extended dwarf2out to output debug section and corresponding relocations directly to object file |



# Future Plans
- This project is still in the testing phase and can be found in the "devel/bypass-asm" branch of the gcc repository. We need to test, polish, and refactor the code and make it good enough to be included in the upstream.
- Support various other types of object files and target architectures. As of now, it only supports ELF on the X86-64 target. 
# Concluding remarks
I have completed almost all the goals we decided on during the community bonding period. I thoroughly enjoyed the work and would be thrilled to keep contributing. I tried getting into open source a few times before and hit a dead end. Participating in GSoC gave me the right confidence and skill to make meaningful contributions. Now, instead of feeling overwhelmed by a big codebase, I have the skills to handle it.
# Acknowledgments
Thanks to Google, GCC, and my mentors for this opportunity. I will be forever indebted to my mentors and GCC community for their constant support and guidance.



