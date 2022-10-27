# TODO

## 参考

🗄 `science.md` electricity
📚
* ✅ Hillis pattern in the stone
* Hyde great code
* Nisan elements
* Petzold code

## current

## queue

* how is BSON more binary than JSON? https://stackoverflow.com/questions/3554325/why-is-it-called-bson 📙 Kleppmann ch. 4
* blog series for Nisan https://github.com/zachvalenta/nand2tetris

## done

* _22_: protocol (encoding, serialization)
* _21_: prefix code
* _14_: Gleick the information
* _11_: Hillis pattern in the stone

# COMPSCI

📙 Conery ch. 1-4

## computation

📚
* MacCormick ch. 10
* Petzold annotated turing

```python
def computation():
    return human_significance(data=hw_automate_math_op(num_sys, logic_gate), encoding)
```

---

* _lambda calculus_: Conery chapter 3 https://www.youtube.com/watch?v=pkCLMl0e_0k https://news.ycombinator.com/item?id=27648871 https://www.youtube.com/watch?v=QuXJ3kXUCiU
* _non-determinism_: https://ahelwer.ca/post/2020-04-15-probabilistic-distsys/

machines
* stack machine, register machine: used in VM design https://tech.davis-hansson.com/p/congress-is-a-vm/
* _finite state machine (FSM)_: machine w/ fixed set of possible states 📙 Conery 66
* input not idempotent e.g. ball point pen https://www.youtube.com/watch?v=4rNYAvsSkwk https://arpitbhayani.me/blogs/fsm https://www.youtube.com/watch?v=nG_ZsNxRz0o
* Jira ticket stages would be another example https://news.ycombinator.com/item?id=24409556 https://github.com/alysivji/finite-state-machine https://github.com/statelyai/xstate
* DFA https://en.wikipedia.org/wiki/Deterministic_finite_automaton
* _halting problem_: a program which could analyse an arbitrary other program and tell if it would halt / stop running cannot exist https://blog.robertelder.org/computer-science-for-engineers/ https://tigyog.app/d/C:tWWwvJDWlo/r/busy-beavers
* _incompleteness theorem_: https://tigyog.app/d/C:tWWwvJDWlo/r/busy-beavers
* _Von Neumann architecture_: model for hardware that allowed for data input via memory vs. rewiring hardware itself https://blog.robertelder.org/computer-science-for-engineers/
* _Turing machine_: Turing complete means computer that can do what a Turing machine can do https://www.youtube.com/watch?v=dNRDvLACg5Q
```python
if state == state359 and current_tape_location == 1:
    current_tape_location == 0
    goto(state247)
# and so on
else state == done:
    render_answer()
    goto(halting_state)
```

## information theory

📚
* MacCormick 9 algorithms
* Gleick information
* https://www.khanacademy.org/computing/computer-science/informationtheory

signal/noise 📙 Gleick ch. 7-8
* _digital_: discrete values for signal representation e.g. light switch 📙 Shibuya 1.31
* _analog_: continuous values for signal representation e.g. light dimmer 📙 Kozeriok 4.62
* _noise_: more important than / independent from bias https://conversationswithtyler.com/episodes/daniel-kahneman/ 🗄 `psychology.md` bias

compression
* _lossy_: data removed in way mostly unnoticed by end user e.g. mp3
* _lossless_: no data rm, original data can be reconstructed e.g. JS minification 📙 Shibuya 1.33
* https://www.destroyallsoftware.com/screencasts/catalog https://go-compression.github.io/ Grudzinski 40
* MacCormick chapter 7
* https://tech.marksblogg.com/minimalist-guide-compression.html

entropy
> got here from "how to create session ID in Python?" 🗄 `http.md` https://stackoverflow.com/questions/817882/unique-session-id-in-python https://unix.stackexchange.com/a/361789
* https://victorzhou.com/blog/information-gain/
* https://aatishb.com/entropy/
* https://www.youtube.com/results?search_query=khan+academy+entropy
* _entropy_: 
* used to build decision trees https://www.freecodecamp.org/news/a-no-code-intro-to-the-9-most-important-machine-learning-algorithms-today/
* _information gain_: 
* _decision tree_: 

## logic gates

🗄 `philosophy.md` logic
📚
* Nisan nand2tetris ch. 1-3
* Petzold code ch. 10-11, 14
* Shibuya microprocessors ch. 1

todo
* Crash Course computer science https://www.youtube.com/playlist?list=PLH2l6uzC4UEW0s7-KewFLBC1D0l6XRfye @ 4 6:45
* https://reasonablypolymorphic.com/book/preface
* Ben Eater https://eater.net/8bit + 📚 Petzold code 17

basics
* _wire_: carries inputs and outputs https://reasonablypolymorphic.com/book/machine-diagrams
* _machine_: transform input to output https://reasonablypolymorphic.com/book/machine-diagrams

gates
* gate/relay - abstraction for controlling current that can implement boolean logical operations
* transistor - gate impl; wire
* _gate_: control path of current https://www.youtube.com/watch?v=gI-qXk7XojA 4:40 🗄 `science.md` engineering / valve
* physical implementation of boolean logic 
* components: wires (input, output)
* _transistor_: current from control wire connects current from two electrodes https://www.youtube.com/watch?v=gI-qXk7XojA 3:10 input (control wire) output (current) germanium  https://www.youtube.com/watch?v=LUXR8UnYhzc 📚 Petzold code 18

operations
* _not_: move output in front of control wire, so input turned on (i.e. control wire touching electrodes) the current will flow to ground and not to output https://www.youtube.com/watch?v=gI-qXk7XojA 4:05
* _and_: two transistors in a row https://www.youtube.com/watch?v=gI-qXk7XojA 5:20
* _or_: two transistors in a parallel https://www.youtube.com/watch?v=gI-qXk7XojA 6:15

# HARDWARE

📚
* Matthews dive https://diveintosystems.org/
* Shibuya microprocessors
* Upton rapsberry pi

firmware
* _firmware_: software tied to hardware
* _BIOS (basic IO)_: firmware that gives option of where to boot from; can boot from vinyl https://news.ycombinator.com/item?id=25177045
* _UEFI_: newer version of BIOS that's apparently more of a pain https://www.youtube.com/watch?v=mxA9Gyyu6Rg 5:45
* _boot_: BIOS -> bootloader (GRUB) -> OS
* _CMOS_: chip that holds BIOS

za
* _acceleration_: hw for specialized tasks e.g. TPU https://en.wikipedia.org/wiki/Hardware_acceleration https://danluu.com/learning-to-program/
* _embedded system_: os for larger mechanical device, probably doesn’t have file system or long-term storage
* _ESP8266_: system on a chip, MicroPython, PikaScript https://news.ycombinator.com/item?id=31433815
* _FPGA_: things you can program with Verilog, VHDL https://danluu.com/why-hardware-development-is-hard/
* _laptop_: non-unibody (easier to repair) unibody (Macbook; harder to switch battery, repair) https://www.netbooknews.com/tips/what-is-a-unibody-laptop/
* _microcontroller_: special-purpose computer, often embedded in another device 📙 Shibuya chapter 6
* _quantum_: used for physics simulations; qubit (like traditional bit 0/1 when observed, but when not observed represents probability of 0/1) https://news.ycombinator.com/item?id=22994468 📚 Gleick 13
* _transparent_: not visible/controllable e.g. L1 cache transparent to compiler https://www.reddit.com/r/compsci/comments/95ns21/what_is_difference_between_register_and_l1_cache/ confusing terminologically https://en.wikipedia.org/wiki/Transparency_(human%E2%80%93computer_interaction)
* _UPS_: uninterruptible power supply (backup juice for proper shutdown)
* circuits, branch prediction https://danluu.com/branch-prediction/

## form factors

📚
* Conery ch. 5

chips
* _silica_: mineral extracted from sand
* _silicon_: element formed by rm oxygen from silica; btw aluminum and phosphorus; by itself only a semiconductor
* _wafer_: larger piece of processed silicon
* _diode_: is a conductor that allows current flow in one direction
* _semiconductor_: https://www.youtube.com/watch?v=qCSIGejNT4M https://twitter.com/szeloof/status/1280249239495479297 https://blog.robertelder.org/semiconductor-example-uses/

chip manufacturing https://doxa.substack.com/p/why-a-chinese-invasion-of-taiwan
* _fabless_: you design, someone else manufacturers (AMD, Nvidia, Qualcomm, Apple) https://www.youtube.com/watch?v=Jyp6jFCzW44
* _foundry_: manufacturing (TSMC, Intel, Samsung, GlobalFoundries) https://stratechery.com/2020/chips-and-geopolitics Intel one of the few that does both design and manufacturing https://stratechery.com/2022/the-intel-split/
* _HDL_: software for designing chips
* ARM has more balance btw battery life and perf, x86 more perf https://diff.substack.com/p/taiwan-and-supply-chain-frenmity
* cloud computing kept Intel going after they lost smartphones https://stratechery.com/2021/intel-problems/
> Intel both designs and makes chips, whereas TSMC mostly makes other people's designs for them - hence it makes Apple's custom ARM-based CPUs for iPhones and now Macs. - Evans 2020.07.28
> After all, nearly all mobile chips are centered on the ARM architecture...It is manufacturing capability, on the other hand, that is increasingly rare...In fact, today there are only four major foundries: Samsung, GlobalFoundries, Taiwan Semiconductor Manufacturing Company (TSMC), and Intel. Only four companies have the capacity to build the chips that are in every mobile device today, and in everything tomorrow. https://stratechery.com/2021/intel-problems/

materials https://www.youtube.com/watch?v=LN0ucKNX0hc
* _relay_: 
* _vacuum tubes_: shift from electro-mechanical to electronic (i.e. no moving parts)
* _transistor_: switch controlled by electricity; like spigot on a tap https://www.youtube.com/watch?v=gI-qXk7XojA 3:00 invented at Bell Labs [Manga 1.32]
* _electrode_: conductor that makes contact w/ nonmetallic part of circuit (like a transistor) https://en.wikipedia.org/wiki/Electrode

timeline
* _1830_: Babbage analytical engine https://www.youtube.com/watch?v=O5nskjZ_GoI 8:45 differential analyzer https://twobithistory.org/2020/04/06/differential-analyzer.html
* _1890_: Hollerith machine (punch cards) for US census (https://en.wikipedia.org/wiki/Domesday_Book) -> became IBM in 1924 https://www.youtube.com/watch?v=O5nskjZ_GoI 10:55
* _1945_: Colussus - first programmable (configured w/ plugs) https://www.youtube.com/watch?v=LN0ucKNX0hc 6:10
* _1946_: ENIAC https://www.youtube.com/watch?v=LN0ucKNX0hc 6:45
* _1950_: IBM mainframes
* _1975_: Altair 8080 https://twobithistory.org/2018/07/22/dawn-of-the-microcomputer.html
* _1984_: Mac https://en.wikipedia.org/wiki/Macintosh#1984:_Debut

## memory

📚
* Arpaci ch. 13-23
* Bryant ch. 6
* Petzold code ch. 16
* Galvin ch. 8-9
🗄
* `language.md` memory
* `linux.md` processes

RAM
* _RAM (random access memory)_: holds program/data until needed by CPU 📙 Manga 1.19, LPI 2.1
* has direction connection to all addresses via memory controller (unlike storage and disk head) https://www.interviewcake.com/article/python/data-structures-coding-interview#ram
* aka working memory https://www.interviewcake.com/article/python/data-structures-coding-interview
> RAM is just bigger-but-slower CPU cache. https://news.ycombinator.com/item?id=25056588
* _address_: location in RAM holding single byte
* untyped (unlike ALU register) https://www.interviewcake.com/article/python3/data-structures-coding-interview#ram
* _memory controller_: thing that reads/writes from memory addresses
* when CPU reads from address controller will also prefetch nearby addresses https://www.interviewcake.com/article/python/data-structures-coding-interview
* _swap file_: free up mem via temp write to disk
> Swapfile is just bigger-but-slower RAM. https://news.ycombinator.com/item?id=25056588

---

bits
* _bit depth_: [Franz 38, 226] bounce (mv from one bit depth to another) [Franz 226] https://reverb.com/news/home-recording-basics-ii-choosing-your-first-audio-interface-and-daw https://www.youtube.com/watch?v=JTtSihQ8QX0 2:45
* _word_: data unit used by architecture, aka digital word [Franz 38] registers and memory are word-sized e.g. 32-bit (90s, x86) 64-bit (00s, ARM64) https://stackoverflow.com/a/9287273 https://www.youtube.com/watch?v=IknbgnJLSRY 1:05 Upton raspberry pi 149 people still use 32-bit on 64-bit https://gankra.github.io/blah/c-isnt-a-language/ https://news.ycombinator.com/item?id=30704642
> Yet, Python integers are interesting because they are not just 32-bit or 64-bit integers that CPUs work with natively. Python integers are arbitrary-precision integers, also known as bignums. This means that they can be as large as we want, and their sizes are only limited by the amount of available memory. https://tenthousandmeters.com/blog/python-behind-the-scenes-8-how-python-integers-work/
* _bit field_: access individual bits in order to save space i.e. instead of normal disregard for storage size of, say, an int, you go and fiddle with how int stored so it doesn't take up as much space as bits normally take in your language (32, 64, whatever) https://www.youtube.com/watch?v=aMAM5vL7wTs
* _bit mask_: pattern of bits that updates another pattern of bits https://www.youtube.com/watch?v=Ew2QnDeTCCE
* _endianness_: order of byte storage https://www.youtube.com/watch?v=OoHich9BPxg https://www.youtube.com/watch?v=NcaiHcBvDR4
* _big endian_: most significant byte at smallest memory address and vice versa https://perldoc.perl.org/perlglossary#big-endian
* _little endian_: least significant byte at smallest memory address https://corecursive.com/066-sqlite-with-richard-hipp/
* _endian_: put most significant bit first or last

big
* _page fault_: attempt to read data from memory but instead forced to go to disk 📙 `evans-linux.pdf` 24
* _virtual memory_: disk used as memory when you run out of actual memory 📙 `evans-linux.pdf` 24 https://questions.wizardzines.com/virtual-memory.html 📙 Bryant (9)
* _swap area_: park of disk used as virtual memory https://serverfault.com/a/48487
* _mmap_: Linux program that maps disk to memory https://brunocalza.me/discovering-and-exploring-mmap-using-go/ 📙 `evans-linux.pdf` 24

* _ROM_: measured in megahertz
* _segmentation fault_: [`evans-linux.pdf` 16]
* _buffer overflow_: buffer writes to adjacent memory instead of intended location; useful to escalate privilege e.g. Morris worm
* _page table_: map of processes to their memory addresses; kernel gives CPU new page table each time it switches processes [`evans-linux.pdf` 16]

## processor

📚
* Christian chapter 5
* Galvin chapter 6
* Tanenbaum chapter 8

---

ALU
* _ALU_: executes on opcode [Manga 1.23] https://en.wikipedia.org/wiki/Arithmetic_logic_unit#Implementation
* _opcode_: operator and operand https://hacks.mozilla.org/2017/02/a-crash-course-in-assembly/ https://tech.marksblogg.com/faster-python.html
* _data path_: how much data moves around circuit e.g. computer data pathes generally 1 byte wide [Petzold 180]
* _cache_: caches RAM for processor, needs a few more cycles to read than registers https://www.reddit.com/r/compsci/comments/95ns21/what_is_difference_between_register_and_l1_cache/e3u4tlt e.g. L1 cache
* _register_: internal to processor i.e. not memory https://stackoverflow.com/a/9287273 size can vary on data type held e.g. 80 bits for floating point

ISA 📙 Bryant ch. 4 https://en.wikipedia.org/wiki/Instruction_set_architecture
* _ISA_: interface for processor 📙 Evans Linux 1, PG hackers and painters 179
* defines processor instructions, virtual memory, etc. https://en.wikipedia.org/wiki/Instruction_set_architecture
* _ARM64_: ARM for desktops
* _x86_: https://github.com/cirosantilli/x86-bare-metal-examples#china
📍 port in notes from 'memory'
* https://drewdevault.com/2021/03/19/A-new-systems-language.html
* ARM, RISC V https://riscv.org/ https://www.youtube.com/watch?v=Lo63uDIiCH0
* https://www.jeffgeerling.com/blog/2020/raspberry-pi-cluster-episode-4-minecraft-pi-hole-grafana-and-more
* https://www.jeffgeerling.com/blog/2020/what-does-apple-silicon-mean-raspberry-pi-and-arm64

scheduling 🗄 `linux.md` processes
* https://wizardzines.com/comics/cpu-scheduling/

* _processor_: aka CPU; can have n cores (i.e. parallelism) https://stackoverflow.com/q/19225859 can only add and subtract [Manga 1.15]
* _core_: main component that reads from memory, maintains execution order and state, and uses ALU to perform operations https://stackoverflow.com/a/19314303 https://testdriven.io/blog/developing-an-asynchronous-task-queue-in-python/
* _core types_: physical (what it sounds like) logical (abstraction to facilitate hyperthreading) https://stackoverflow.com/q/1715580 https://forums.tomshardware.com/threads/what-is-the-difference-between-physical-core-and-logical-core.1534416/
* _hyperthreading_: single core that can execute n instructions simultaneously
* _GPU_: https://news.ycombinator.com/item?id=23986925 https://lwn.net/Articles/827596/
* _Apple silicon_: processor that uses ARM64

❓ how do chips relate to processor
* _chip_: piece of silicon holding approx B transistor; made by Intel, ARM, AMD, Qualcomm
* _processor_: main chip
* _chip set_: other chips that help out processor
* _motherboard_: aka PCB; holds chips; made of fiberglass
* _trace_: copper wires carrying electricity around PCB

operations
* _clock speed/rate/cycle_: interval at which processor can do something; ARM (1 clock cycle per instruction; efficient) x86 (n clock cycle per instruction; performant)
* _speed_: measured in gigahertz i.e. how many billion cycles happen per second; base speed and turbo https://www.bhphotovideo.com/explora/computers/tips-and-solutions/boost-processors
* _idling_: entering a lower power stage when no instructions to execute; cost to enter/exit idle, so don't want to do for overly short periods

* modern microprocessors https://news.ycombinator.com/item?id=27014027

## storage

📚
* Galvin 10
* Tanenbaum 5.4
* Arpaci ch. 36-45

* _storage_: slower access (vs. mem)
* _disk_: slower than memory, more space https://www.interviewcake.com/article/python3/data-structures-coding-interview typically cheaper than RAM [Kleppmann 88]
* _platter_: storage medium
* _head_: thing that reads/write from platter; sequential access because has to physically move across platter https://www.interviewcake.com/article/python/data-structures-coding-interview#ram
> In the ’80s and ’90s, our hard drives were essentially optimized record players, with a read head riding on top of a spinning platter. - https://www.moderndescartes.com/essays/data_oriented_python/
* _actuator_: moves about for head to read
* _sector_: 类似 attribute
* _block_: 类似 record https://ownyourbits.com/2018/05/02/understanding-disk-usage-in-linux/ aka 'cluster'
* _slack space_: unused blocks
* _how is data stored?_ don’t need to be contiguous i.e. OS keeps track of what is where [Think OS 4.2]
* _content-addressed storage (CAS)_: store using cryptographic hash as key [Itamar 'software is a means not an end']
* _defragment_: putting things in same file closer together on platter [Franz 82]

* storage medium
| type      | full name   | notes                     
| --------- | ----------- | -------------------------
| HDD       | hard disk   | slowest (2-6 ms to read   
| SSD       | solid state | faster                    
| SSHD      | hybrid      | HDD w/ 16GB of SSD        
| flash     | -           | fastest; non-volatile RAM 
| long-term | -           | https://archiveprogram.github.com/ https://spectrum.ieee.org/computing/hardware/why-the-future-of-data-storage-is-still-magnetic-tape
| --------- | ----------- | ------------------------- 

# PROTOCOLS

🔍 https://format.wtf/examples
📙
* Bhargava ch. 5
* MacCormick ch. 4
🗄
* `security.md` cookies, encryption
* `sociology.md` linguistics

semantics
* _protocol_: fmt https://blainsmith.com/articles/plain-text-protocols/
* "implement protocol/spec" = create library for language to read/write data in that protocol https://msgpack.org/ https://github.com/polyglotted/msgpack-python/tree/master/msgpack https://github.com/aviramha/ormsgpack https://bsonspec.org/faq.html https://bsonspec.org/spec.html
* _serialization_: convert obj to protocol for network transmission 📙 Kleppmann 113
* _encoding_: protocol to represent non-digital (text, audio) as digital 📙 Petzold ch. 20
* i.e. binary files don't have encoding themselves but have text fields w/ encoding https://stackoverflow.com/a/38264655
* synonym for conversion in general e.g. Morse code dot/dash to electrical signal 📙 Sweigart ciphers 3 https://www.reddit.com/r/AskProgramming/comments/c8pssr/comment/esom0gi/

## encoding

https://en.wikipedia.org/wiki/Mojibake
https://docs.python.org/2/howto/unicode.html
https://docs.python.org/3/howto/unicode.html
https://lucumr.pocoo.org/2014/1/5/unicode-in-2-and-3/

📍 utf-8 vs. unicode https://youtu.be/SM9gJv08dm0 2:30 https://stackoverflow.com/questions/643694/what-is-the-difference-between-utf-8-and-unicode https://nbviewer.org/gist/guocheng/1ae6c2d76461a66cfc5ec6009b5791d1 https://docs.python.org/3/howto/unicode.html

```sh
# app reads bytes from disk
1101000 1100101 1101100 1101100 1101111 
# app uses UTF-8 to decode
104 101 108 108 111 
# app uses Unicode
"hello"
```

character set
* _Unicode_: character set https://stackoverflow.com/a/13212528
* i.e. way to identify each character uniquely https://practicaltypography.com/ligatures-in-programming-fonts-hell-no.html
* _character set_: KV set in which K = characters and V = code point e.g. A = 41
* _code point_: numerical value in character set e.g. `0x0394`
* file types have https://the.exa.website/features/icons

encoding
* UTF-8: encoding
* encoding: algo that transforms number to binary and vice versa
```python
def utf8(num):
    return binary

utf8(1)  # 00000001
utf8(2)  # 00000010
utf8(3)  # 00000011
utf8(4)  # 00000100
```

digraphs
* digraph: two letters forming single phoneme e.g. "ea" in "bread"
* __digraph__: Unicode char not on typical keyboard e.g. °∆ http://vimdoc.sourceforge.net/htmldoc/digraph.html#digraph-table
* specified in RFC 1345 https://datatracker.ietf.org/doc/html/rfc1345
* `^M` = newline/carriage return

---

* _iconv_: convert encoding https://kadekillary.work/post/cli-4-ds/
* emoji https://darrenburns.net/posts/unicode-emoji/
* _encode_: 动 convert to diff fmt 📙 MacCormick 5.66
* typically byte per/char https://stackoverflow.com/a/31322359
> Each byte represents some text character in the program. 📙 Bryant 1.1
* multibyte = n byte per/char e.g. Japanese 📙 Beaulieu 2.19
* can be anything e.g. Morse code (dot/dash to text) 📙 Sweigart 1.3
* QR/bar code https://boonepeter.github.io/posts/2020-11-10-spotify-codes/ https://news.ycombinator.com/item?id=32837565&utm_term=comment
* _decode_: 动 convert back to original fmt https://stackoverflow.com/a/31322359
```yaml
1: "A"  # encode
"A": 1  # decode
```
* _encoding_: 名 spec for how to encode
* e.g. mp3 spec for how to encode audio 📙 Sweigart 1.3
* _character set_: alphabet + syllabary https://en.wikipedia.org/wiki/Character_encoding#Terminology 🗄 `sociology.md` linguistics/grammar
* used synonymously with 'encoding'
> When I discovered that the popular web development tool PHP has almost complete ignorance of character encoding issues, blithely using 8 bits for characters, making it darn near impossible to develop good international web applications, I thought, enough is enough. https://www.joelonsoftware.com/2003/10/08/the-absolute-minimum-every-software-developer-absolutely-positively-must-know-about-unicode-and-character-sets-no-excuses/

prefix codes https://gist.github.com/joepie91/26579e2f73ad903144dd5d75e2f03d83
* _prefix code_: encoding mechanism
```yaml
161133
```
* _codeword_: individual values
* cannot share prefix e.g. `[3, 11, 22]` valid but `[1, 11, 22]` invalid bc `1` and `11` share prefix
* decode prefix code by applying codewords
```yaml
# prefix
161133
# codewords
[1, 2, 33, 50, 61]

# must be 1 bc no other codeword can start w/ 1
1 61133
# and so on for rest
1 61 1 33
```

semantics https://stackoverflow.com/a/41217889
* _protocol_: encoding for computer networking https://blainsmith.com/articles/plain-text-protocols/
* impl can interact; e.g. HTTP - JS client can talk to Python server

* overlap with linguistics https://www.unicode.org/versions/Unicode14.0.0/appE.pdf
* representing integers, Google had to switch from 32-bit to 64-bit for Gangnam Style https://www.interviewcake.com/article/python3/data-structures-coding-interview#fixed-width-nums https://danielmiessler.com/study/encoding/ https://kunststube.net/encoding/ https://kunststube.net/frontback/ https://www.joelonsoftware.com/2003/10/08/the-absolute-minimum-every-software-developer-absolutely-positively-must-know-about-unicode-and-character-sets-no-excuses/
* _base64_: 🗄 `4-application.md` 'headers' https://developer.mozilla.org/en-US/docs/Web/HTTP/Authentication#Authentication_schemes
* _ASCII_: mapping from number to glyph (char) 📍 Petzold 15.181, computerphile 📚 Petzold code ch. 20 https://www.youtube.com/watch?v=XaGXPObx2Gs from pre 8-bit era; `man ascii` https://increment.com/programming-languages/unplain-text-primer-on-non-latin/ can use hex as repr https://github.com/GNOME/ghex
* _UTF8_: multi-byte i.e. characters outside of English just get more bytes thrown at them https://sethmlarson.dev/blog/utf-8 https://news.ycombinator.com/item?id=30259097
* _Unicode_: char set https://stackoverflow.com/a/13212528/6813490 https://github.com/arp242/uni https://www.youtube.com/watch?v=MijmeoH9LT4 https://rentafounder.com/how-to-count-unicode-string-characters/ https://www.dampfkraft.com/ghost-characters.html code point, glyph, octal, hex https://realpython.com/courses/python-unicode/ `unicode-standard.pdf` https://www.joelonsoftware.com/2003/10/08/the-absolute-minimum-every-software-developer-absolutely-positively-must-know-about-unicode-and-character-sets-no-excuses/ https://en.wikipedia.org/wiki/Code_point
* _code point_: char https://en.wikipedia.org/wiki/Code_point https://www.joelonsoftware.com/2003/10/08/the-absolute-minimum-every-software-developer-absolutely-positively-must-know-about-unicode-and-character-sets-no-excuses/ 
* _EOF_: not a char https://ruslanspivak.com/eofnotchar/
* _error correction_: 📙 MacCormick 5 https://en.wikipedia.org/wiki/Error_detection_and_correction

## numeral systems

📚
* Bryant computer systems ch. 2
* Petzold annotated turing
* Petzold code ch. 7-9
* Shibuya microprocessors ch. 1

semantics
* _number_: idea used for proofs https://en.wikipedia.org/wiki/Number
* _numeral system_: math notation for representing numbers
* more symbols = less space e.g. hex requires less places than binary
* _radix (base)_: number of digits in number system 📙 Petzold code 186
* fewer number of states = less ambiguity i.e. we don't use ternary or quinary for transistor 📙 Kozeriok 4.63 https://www.youtube.com/watch?v=gI-qXk7XojA 1:20
* _digit_: symbol to represent a number https://en.wikipedia.org/wiki/Numerical_digit

| system      | radix         | repr of 231 | use [Petzold code 181]
| ----------- | ------------- | ----------- | ---------------------------------------- |
| binary      | two (0-1)     | 1110111     | precise                                  |
| decimal     | ten (0-9)     | 231         | readable                                 |
| hexademical | sixteen (0-f) | e7          | easy converion to binary (unlike decimal)|
| ----------- | ------------- | ----------- | -----------------------------------------|

binary 📚 Petzold code 3, 9, 12-13
* _bit_: binary digit; aka 'flag' [Kozierok 4.63]
* _bitmask_: toggling bit https://www.arp242.net/bitmask.html set (to 1) reset/clear (to 0) [Kozierok 4.63]
* _nybble_: 4 bits [Petzold code 181]
* _byte_: 8 bits
* aka octet https://stackoverflow.com/a/21463473/6813490
* 255 possible values https://www.youtube.com/watch?v=dPxCGlW9lfM 5:10
* _byte string_: sequence of bytes https://stackoverflow.com/a/31322359
* _kilobyte_: 1k bytes
* other sizes: MB, GB, TB, petabyte (1024 tb) exabyte (1B GB) https://stackoverflow.com/a/1241234 [Kozierok 4.63]
* _bit width_: number of bits needed to represent an int e.g. on Intel processors ints are 4 bytes wide https://boredzo.org/pointers/#starting
* add by carrying over e.g. 1 + 1 = 10 [Manga 1.43]
* _two's complement_: how to do substraction on binary, represent negative numbers [Petzold code 15.180, Petzold code 12-13 Manga 1.44-46]
* _high-order bit (MSB)_: bit position w/ greatest value e.g. in 101 the eighths position is the MSB https://en.wikipedia.org/wiki/Bit_numbering also used to mean "most salient point"  https://danluu.com/corp-eng-blogs/ https://diff.substack.com/p/big-tech-sees-like-a-state

decimal in binary
* _unsigned_: positive
* _signed_: positive and negative; can reserve leftmost bit for sign https://www.interviewcake.com/article/python3/data-structures-coding-interview#binary-numbers
* _fixed width_: has specific size e.g. 32 or 64 bits https://www.interviewcake.com/article/python3/data-structures-coding-interview#fixed-width-nums
* _floating point_: 1,230,000 as 1.23 (significand) * 10^6 (exponent) w/ significand as always greater than 1 but less than 2 [manga 42-3]; faster for CPU computation; makes getting a high-level language to behave like your desktop calculator more difficult than you'd expect https://stefanoborini.com/why-01-plus-02-is-not-03-in-python/ https://docs.python.org/3/tutorial/floatingpoint.html https://stackoverflow.com/a/46700365/6813490 https://stackoverflow.com/a/50340297/6813490 https://0.30000000000000004.com/ fractions also get weird, too https://orbifold.xyz/numbers.html 📜 Van Rossum ch. 8
> https://ciechanow.ski/exposing-floating-point/
```python
value = 0.1 + 0.2
f"{val:.{1}}"  # 0.3
val = 45 * (0.1 + 0.2)
f"{val:.{4}}"  # 13.5
```

hex 📚 Petzold code ch. 15
* _hexit_: hex digit (1 nybble) https://www.youtube.com/watch?v=dPxCGlW9lfM 4:30
* used bc easier to convert to binary than decimal [Petzold code 181 https://www.youtube.com/watch?v=dPxCGlW9lfM 4:20]
* _viewer_: https://github.com/sharkdp/hexyl https://github.com/WerWolv/ImHex `hexdump -C <file>` https://www.youtube.com/watch?v=-eDY7yh-CyA 1:50
* _editor_: online https://hexed.it/ macOS https://ridiculousfish.com/hexfiend/ hexedit https://news.ycombinator.com/item?id=23762626

## serialization

📙 Kleppmann ch. 4
🗄
* `shell.md` design
* `sql.md` munge/sanitization

semantics
* _serialization_: encoding for data interchange 📙 Kleppmann [115]
* no one uses language-specific versions e.g. Pickle 📙 Kleppmann [114]
* _unstructured text_: e.g. Unix tools
* flexible http://www.catb.org/~esr/writings/taoup/html/ch05s01.html https://news.ycombinator.com/item?id=23630640
* leads to complexity https://danluu.com/cli-complexity/ 
* _structured text_: e.g. Powershell, JSON, CSV, XML, HTTP/1 https://news.ycombinator.com/item?id=27431998
* operating systems use of https://news.ycombinator.com/item?id=28301646

JSON 📜 http://www.json.org/ https://seriot.ch/projects/parsing_json.html https://github.com/burningtree/awesome-json
* objs: colloquially (start/end w/ braces) https://youtu.be/SM9gJv08dm0 0:30 literally (doesn't exist) http://benalman.com/news/2010/03/theres-no-such-thing-as-a-json/
* typing: str, bool, array, num (int/float considered the same, which can be problem w/ large numbers) 📙 Kleppmann [144]
* no comments https://stackoverflow.com/a/4183018
* no binary strings 📙 Kleppmann [144]
* history https://twobithistory.org/2017/09/21/the-rise-and-rise-of-json.html
* as output for Unix utils https://blog.kellybrazil.com/2019/11/26/bringing-the-unix-philosophy-to-the-21st-century/ https://github.com/kellyjonbrazil/jc https://news.ycombinator.com/item?id=22608045
* for sharing logic btw frontend/backend https://news.ycombinator.com/item?id=27306263
```json
// one-liner
{"a": "b"}

// full
{
    "topLevel": "val",
    "myList": [1,2,3],
    "topObj": {
        "foo": false
    }
}
```
* fmt: `python3 -m json.tool music-lib.json > music-lib-fmt.json` https://orbifold.xyz/check-in-json.html
* query: jq https://github.com/stedolan/jq 🗄 `db.md` SQLite / CLI
* viewer: jless https://jless.io/ https://github.com/gulyasm/jsonui
```sh
# goto: H parent g top gg btm
# collapse: SPACE/h
# collapse all: c
# expand: SPACE/l
# scroll: j/k (children) J/K (parents)
# page: CTRL d/u
# center: zz
```
```sh
# https://earthly.dev/blog/jq-select/ https://github.com/noahgorstein/jqp https://sequoia.makes.software/parsing-json-at-the-cli-a-practical-introduction-to-jq-and-more

```
* generate: https://github.com/jpmens/jo https://github.com/jazzband/tablib
* diff: graphtage https://github.com/trailofbits/graphtage
* edit: dasel https://github.com/TomWright/dasel deepdiff https://news.ycombinator.com/item?id=33136351
* convert: rq https://github.com/dflemstr/rq

csv 🗄 `db.md` munge
* editor https://www.moderncsv.com/
* diff https://github.com/aswinkarthik/csvdiff
* _DSV_: same as `.dat` https://en.wikipedia.org/wiki/Delimiter-separated_values https://www.thoughtspot.com/blog/csv-vs-delimited-flat-files-how-choose
* no firm spec https://peps.python.org/pep-0305/#abstract
* gaining in popularity https://twobithistory.org/2017/09/21/the-rise-and-rise-of-json.html#fnref:2 
* some parsers don't impl escaping rules correctly 📙 Kleppmann 4.145
* comments: no standard from RFC 4180, parser can set https://stackoverflow.com/a/14428538 https://stackoverflow.com/a/1961018
* _header line_: line with col names https://miller.readthedocs.io/en/latest/glossary/#header-line
* _data line_: line with data https://miller.readthedocs.io/en/latest/customization/
* _field_: value, either in header line or data line https://miller.readthedocs.io/en/latest/10min/#handling-field-names-with-spaces
* header not always first line, detection non-trivial https://news.ycombinator.com/item?id=28299015

binary
* e.g. HTTP/2 https://news.ycombinator.com/item?id=27431998
* formats: Thrift, Protocol Buffers, Avro 
* db res in binary which is parsed by language-specific API 📙 Kleppmann 4.128
📙 Kleppmann 4.117, 4.122, 4.130
* _Avro_: serialization format https://avro.apache.org/docs/current/
* better than CSV bc handles typing, cells missing data
* CSV disadvantages: inferred data types https://www.youtube.com/watch?v=SZX9DM_gyOE 1:20
* SQL disadvantages: flat
* competes with Thrift, Protocol Buffers https://avro.apache.org/docs/current/
* Python tutorial https://avro.apache.org/docs/current/gettingstartedpython.html
* https://www.youtube.com/watch?v=kq_JCVcHJLE
* _BSON_: binary JSON + SQL datatypes https://bsonspec.org/
* can be less space efficient due to datatypes https://en.wikipedia.org/wiki/BSON#Efficiency
* faster to parse https://bsonspec.org/faq.html
* datatypes: JSON + date, binary, num (int, long, float) https://youtu.be/SM9gJv08dm0 2:25
* _MessagePack_: like BSON https://msgpack.org/ 📙 Kleppmann 4.116
* _Protocol Buffers_: like BSON https://bsonspec.org/ https://github.com/bufbuild/buf
* _Thrift_: 

Parquet
* _Parquet_: column-oriented file format, like CSV https://www.youtube.com/watch?v=H_dLfHETO0g
* easier to use now vs. CSV https://news.ycombinator.com/item?id=30595026
* use to build no-code API https://tech.marksblogg.com/roapi-rust-data-api.html

XML
* element types: prolog, root node/element, child node/elements
* _XSLT_: CSS for XML
* _XPath_: CSS selector for XML
* comments: same as HTML
* good for trees (like JSON) https://engineering.instawork.com/when-xml-beats-json-ui-layouts-53c7f1d3fdb7
* previously more popular 📙 Beaulieu 2.34

YAML
* query https://github.com/mikefarah/yq
* _CUE_: alternative https://dagger.io/ CI https://news.ycombinator.com/item?id=30857012

TOML https://toml.io/en/
* comment: `#`
