---
Tags: 
Created: 2023-03-19 16:31:40
---
(Links:: [[Computer Organization]])
# Basic Concepts
- The maximum size of memory that can be used in a computer is determined by the addressing scheme.
- Computers with 16-bit addresses can address up to 64K memory locations.
- Machines with 32-bit addresses can utilize memory that contains up to 4G locations.
- Machines with 64-bit addresses can access up to 16E locations.
- The memory is usually designed to store and retrieve data in word-length quantities.
- The processor uses address, data, and control lines to specify memory locations and transfer data.
- The control lines carry the command indicating a Read or Write operation, as well as the timing information.
- The MFC signal is the processor's internal control signal indicating that the requested memory operation has been completed.
- *Memory access time* measures the time it takes for a memory unit to transfer a word of data
- *memory cycle time* is the minimum delay between two successive memory operations.
- A *random-access memory* (RAM) has the same access time to any location, while serial access storage devices have varying access times.
## Cache and Virtual Memory
- The memory access time can be a bottleneck in computer systems -> processor can process instructions and data faster than they can be fetched from memory
- Cache memory is a small, fast memory inserted between the main memory and the processor to hold currently active portions of a program and their data -> helps reduce the memory access time
- Virtual memory: only active portions of a program are stored in the main memory, while the rest is stored on a secondary storage device -> program sees a memory that is larger than the computer's physical main memory

## Block Transfers
- Data transfers between main memory, cache, and disks occur in contiguous blocks of tens, hundreds, or thousands of words, as well as with high-speed devices like graphic displays or Ethernet interfaces
# Semiconductor RAM Memories
## Internal Organization of Memory Chips
- Memory cells are usually organized in arrays, with each cell capable of storing one bit of information
- The cells in each column are connected to a Sense/Write circuit by two bit lines, and the Sense/Write circuits are connected to the data input/output lines of the chip
- Memory circuits can be organized in different ways, such as a 16 x 8 organization or a 1K x 1 organization
- Larger memory chips have essentially the same organization as small ones, but with a larger memory cell array and more external connections
## Static Memories
- *static memories*: retain their state as long as power is applied.
- [[A static RAM cell.png]]
- **Read operation**: word line is activated; if the state is 1, then line $b$ is in state 1
- **Write operation**: Sense/Write circuit drives lines $b$ and $b'$ and activates word line
- **Cmos Cell**: low power consumption, since current flows in the call when is is being accessed
## Dynamic RAMs
- Static RAM (SRAM) cells are fast but require multiple transistors
- Dynamic RAM (DRAM) cells are less expensive and higher density but do not retain their state for a long period unless accessed frequently
- DRAM stores information in a capacitor charge that can only be maintained for tens of milliseconds, and contents must be periodically refreshed by restoring the capacitor charge to its full value
- DRAM cells consist of a capacitor and a transistor to store information by turning on the transistor and applying an appropriate voltage to the bit line
- DRAM contents must be read before the charge in the capacitor drops below a threshold value, which automatically refreshes the contents
- A 256-Megabit DRAM chip is organized in a 16K x 16K array, and 14 address bits are needed to select a row and another 11 bits to specify a group of 8 bits in the selected row, totaling a 25-bit address to access a byte
- The row and column addresses are multiplexed on 14 pins to reduce the number of external connections, and the RAS and CAS control signals are active when low in commercial DRAM chips
- The timing of DRAM operation is controlled by the RAS and CAS signals generated by an external memory controller circuit when the processor issues a Read or Write command, and the memory controller is responsible for refreshing the data stored in the memory chips.
- [[Internal organization of a 32M x 8 dynamic memory chip.png]]
### Fast Page Mode
- Each sense amplifier acts as a latch, when row address is applied, contents of all cells in selected row are loaded into corresponding latches
- All bytes in selected row can be transferred in sequential order using consecutive sequence of column addresses under the control of successive CAS signals
- Block transfer capability is referred to as the fast page mode feature
## Synchronous DRAMs
- Synchronous DRAMs (SDRAMs) have their operation synchronized with a clock signal
- SDRAMs incorporate control circuitry on the chip that provides many useful features, such as built-in refresh circuitry and buffered address and data connections
- SDRAMs have several modes of operation that can be selected by writing control information into a mode register
- Burst operations of different lengths can be specified, and it is not necessary to provide externally-generated pulses on the CAS line to select successive columns
- SDRAMs can deliver data at a very high rate, because all the control signals needed are generated inside the chip
- SDRAMs operate with clock speeds that can exceed 1 GHz
### Latency and Bandwidth
-  Memory latency is the time it takes to transfer the first word of a block.
- The time required to transfer a complete block depends on the rate at which successive words can be transferred and on the size of the block.
- The number of bits or bytes that can be transferred in one second is known as memory bandwidth.
- Memory bandwidth depends on the speed of access to the stored data and on the number of bits that can be accessed in parallel.
### Double-Data-Rate SDRAM
- large number of bits are accessed at the same time inside the chip when a row address is applied
- data transfered on rising and falling edges of the clock -> *double-data-rate SDRAMs* (DDR SDRAMs)
- DDR2 and DDR3 can operate at clock frequencies of 400 MHz and 800 MHz respectively.
- DDR2 and DDR3 can transfer data using effective clock speeds of 800 MHz and 1600 MHz respectively.
### Rambus Memory
- Rambus technology provides a high-speed interface between memory and processor for high data transfer rate.
- differential-signaling technique: signals are transmitted using small voltage swings of 0.1 V above and below a reference value
## Structure of Larger Memories
### Static Memory Systems
- [[Organization of a 2M x 32 memory module.png]]
- [[512 x 8 static memory chip.png]]
- Each column implemnets one byte position in a word with four chips providing 2M bytes
- Twenty-one address bits are needed to select a 32-bit word in this memory
- The high-order two bits of the address are decoded to determine which of the four rows should be selected
- Remaining 19 address bits are used to access specific byte locations inside each chip in the selected row
- The R/W inputs of all chips are tied together to provide a common Read/Write control line
### Dynamic Memory Systems
- Available dynamic RAM chips have capacities as high as 2G bits and even larger chips are being developed.
- Memory chips may be organized to read or write a number of bits in parallel to reduce the number of memory chips needed in a given computer.
- Memory modules are developed to house many memory chips on a small board that plugs into a socket on the computer's motherboard.
- Memory modules are commonly called SIMMs or DIMMs depending on the configuration of the pins.
- Different sized memory modules can use the same socket to easily expand total memory capacity.
### Memory Controller
- Dynamic RAM (DRAM) address has two parts: high-order bits select a row and low-order bits select a column.
- A memory controller is required to manage the DRAM operation, including multiplexing the address and generating RAS and CAS signals.
- The memory controller selects one of the memory modules based on the high-order bits of the address.
- Data lines connect the processor and the memory directly.
- DRAM needs to be refreshed periodically, and synchronous DRAM has the circuitry included to initiate the refresh cycles, while asynchronous DRAM requires a control circuit external to the chip to initiate the refresh cycles.
### Refresh Overhead
- Dynamic RAM needs internal refresh operation before responding to read or write requests
- Requests are delayed until the refresh cycle is completed
- Time lost to accommodate refresh operations is very small
- Refresh overhead for an SDRAM is less than 1 percent of the total time available for accessing the memory
- Refresh operations are arranged such that all rows of the chip are refreshed in 8K (8192) refresh cycles
### Choice of Technology
- Factors affecting choice of RAM chip: cost, speed, power dissipation, and size.
- Static RAM: fast operation, but expensive and low bit density due to complex circuitry.
	- Used where small, fast memory is needed.
- Dynamic RAM: high bit densities and low cost per bit.
- Synchronous DRAMs commonly used for implementing main memory.
# Read-only Memories (ROM)
- normal operation involves only reading the stored data -> ROM
## ROM
- information can be written into it only once at the time of manufacture

![[A ROM cell.png|500]]
- logic value 0 is stored in the cell if the transistor is connected to ground $P$, otherwise a 1 is stored
## PROM (programmable)
- user can insert 1s at the required locations by burning out the fuses at point $P$ using high-current pulses -> irreversible
- memory chips can be programmed directly by the user
## EPROM (erasable)
- connection to ground point $P$ through special transistor
	- turned off creating open switch
	- turned on by injecting charge that becomes trapped
- erase by exposing the chip with ultraviolet light
- must be removed for erasure, and erases entire contents
## EEPROM (electrically erasable)
- different voltages needed for erasing, writing and reading the stored data
## Flash Memory
- you can only write an entire block of cells
- high density, little power supply voltage and consume less power
- attractive for use in portable, battery-powered equipment
# Direct Memory Access
- transfer blocks of data directly between the main memory and I/O devices without continuous intervention by the processor (DMA controller)
- DMA controller: performs functions (normally by processor) when accessing main memory
	- provide memory address for each word transferred
	- generates control signals needed
	- increments memory address for successive words
	- keeps track of number of transfers
- processor sends starting address, number of words, and direction of transfer to DMA controller -> raises interrupt when finished
# Memory Hierarchy
- [[Memory hierarchy.png]]
- registers are at the top in terms of speed of access
- *processor cache*: holds copies of the instructions and data stored in a much larger memory that is provided externally
- cache is located on processor chip
- multiple levels of cache with different speeds and sizes
- *main memory*: assembled in memory modules such as [[#Dynamic Memory Systems|DIMMs]]
	- much larger but slower than cache
# Cache Memories
- *locality of reference*: main memory appears faster to the processor than it actually is
- many instructions in localized areas of the program are executed repeatedly during some time period
	- temporal: recently executed instruction is likely to be executed again very soon
	- spatial: instructions close to a recently executed instruction are also likely to be executed soon
- temporal locality: when information/data/instruction is needed, bring it into cache because it will likey be needed again
- Spatial locality: fetch not one but several items
- block of memory transfered into cache on read request
	- correspondence between main memory block and those in cache specified by *mapping function*
	- block removed for creating space for new block decided by caches *replacemnet algorithm*
### Cache Hits
- processor doesn't know if data is memory or cache -> if the requested data is in cache: *read* or *write hit*
- Write operation
	- *write-through*: cache location and main memory location are updated ^74f904
	- *write-back*: update cache location with *dirty/modified bit* and update main memory once block is removed from cache ^e84a34
- write-through easier to implement than write-back but unneccesary
### Cache Misses
- word is not in the cache -> *read miss*
	- block of words containing request copied into cache
	- *load-through*: word sent to processor directly once read from memory
	- processors use separate cahces for instructions and data -> no halt delay pipelining
## Mapping Functions
### Direct Mapping
- block $j$ of the main memory maps onto block $j\% 128$ of the cache
- placement of a block in the cache is determined by its memory address
- main memory address:
	- lower-order 4 bits: select one of 16 words in a block
	- 7-bit cache block: determine cache position to save the block at
	- high-order 5 *tag* bits: identify one of the 32 main memory blocks mapped into the current cache position
- high-order 5 bits of address are compared with tag bits associated with cache location
	- match -> desired word is in block of the cache

> [!tip] Calculating memory address bits
> $$\text{Word bits}=log_2(\text{Words in a block})=log_2\left(\frac{\text{Bytes per block}}{\text{Bytes per Word}}\right)$$
> $$\text{Block bits}=log_2(\text{Blocks in cache})$$
> $$\text{Tag bits}=log_2\left(\frac{\text{Blocks in memory}}{\text{Blocks in cache}}\right)$$
### Associative Mapping
- any memory block can be put into any cache block
- high-order 12 bits used to compare memory address with cache address
- replacement only when cache is full
- parallel search of the cache: *associative search* 

> [!tip] Calculating memory address bits
> $$\text{Word bits}=log_2(\text{Words in a block})=log_2\left(\frac{\text{Bytes per block}}{\text{Bytes per Word}}\right)$$
> $$\text{Tag bits}=log_2(\text{Blocks in memory})$$
### Set-Associative Mapping
- blocks of cache grouped into sets
- block may be placed in a specific set

> [!example]
> - 4096 memory blocks
> - 128 cache blocks
> - 64 cache sets -> blocks can map into one of two block positions within a set
> - 6-bit set field in the address determines which set of the cache might contain the desired block

- a cache that has $k$ blocks per set is referred to as a $k$-way set-associative cache

> [!tip] Calculating memory address bits
> $$\text{Word bits}=log_2(\text{Words in a block})=log_2\left(\frac{\text{Bytes per block}}{\text{Bytes per Word}}\right)$$
> $$\text{Set bits}=log_2(\text{Sets in cache})$$
> $$\text{Tag bits}=log_2\left(\frac{\text{Blocks in memory}}{\text{Sets in cache}}\right)$$

> [!tip] Sets in cache
> $$\text{Sets in cache}=\frac{\text{Bytes in the cache}}{\text{Bytes per Block}\times K}$$
### Stale Data
- *valid bit*: indicates whether data in the block is valid
	- initially set to 0 when power is applied 
	- may be set to 0 when new programs or data are loaded
- the processor fetches data from a cache block only if its valid bit is equal to 1
- *flushing* the cache: forcing all dirty blocks to be written back to the memory before performing the transfer to disk
- *cache-coherence*: two different entities use identical copies of data
## Replacement Algorithm

> [!important] Least Recently Used (LRU) algorithm
> high probability that blocks referenced recently are referenced again soon -> overwrite block that has gone the longest time without being referenced
- cache controller tracks refernces to all blocks
- 2-bit counter for a four-block set
	- block referenced (cache hit)-> counter set to 0
		- counters with values originally lower incremented
	- counter associated with new block (cache miss, set not full) -> counter set to 0
		- all other counters incremented
	- counter with value 3 removed (cache miss, set is full)
- small amount of randomness in deciding with block to replace can improve performance
# Performance Considerations
## Hit Rate and Miss Penalty
- *hit rate*: number of hits stated as a fraction of all attempted accesses
- performance affected by actions that need to be taken when a miss occurs
- *miss penalty*: total access time seen by the processor when a miss occurs
- $h$: hit rate
  $M$: Miss penalty
  $C$: time to access information in the cache
$$t_{avg}=hC+(1-h)M$$

> [!example]+ 
> - access times to cache and main memory are $\uptau$ and $10\uptau$ respectively
> - block of 8 words transferred in $10\uptau$ and remaining 7 words transferred at one word every $\uptau$ seconds
> - miss penalty and load word from cache into processor take $\uptau$ each
> - Miss penalty: $$M=\uptau + 10\uptau + 7\uptau + \uptau=19\uptau$$
> - 30 percent are Read and Write operations -> 130 memory access per 100 instructions
> - hit rates for instruction is 0.95 and 0.9 for data
> - Memory performance improvement: $$\frac{\text{Time without cache}}{\text{Time with cache}}=\frac{130 \times 10\uptau}{100(0.95\uptau+0.05\times19\uptau)+30(0.9\uptau+0.1\times 19\uptau)}=4.7$$
> - Increase in memory access time caused by misses in the cache: $$\frac{\text{Time for real cache}}{\text{Time for ideal cache}}=\frac{100(0.95\uptau+0.05\times 19\uptau)+30(0.9\uptau+0.1\times 19\uptau)}{130\uptau}=2.1$$

## Caches on the Processor Chip
- two separate L1 caches, one for instructions and another for data
- larger L2 cache
- L1 are very fast -> determine memory access time seen by the processor
- L2 are larger to ensure high hit rate
- average access time experienced by a processor with L2 cache: $$t_{avg}=h_1C_1+(1-h_1)(h_2C_2+(1-h_2)M)$$

## Other Enhancements
- **Write Buffer**: 
	- write-through allows Write operatio to write value into main memory
	- processor places each Write request into buffer and continues execution
	- contents of Write buffer sent to main memory when not in responding to Read requests
	- read request might refer to data in Write buffer -> address of data read from memory compared with addresses fo data in Write buffer
	- new block has to be brought into cache -> dirty block in cache might be overwriten -> stored in Write buffer temporarily so new block can be read
	- contents of buffer are written into main memory
- **Prefetching**:
	- avoid stalling processor by prefetching data into cache before they are needed
	- prefetching takes place while processor is busy executing instructions that do not result in a Read miss
	- prefech instructions increase length of programs
	- prefetched data will not be used if ejected from cache by Read miss involving other data
- **Lockup-Free Cache**: 
	- servicing a miss causes cache to be locked
	- *lockup-free*: cache supports multiple outstanding misses -> additional circuitry must keep track of misses

# Virtual Memory
- the processor references instructions and data in an address space that is independent of the available physical
- binary addresses are called *virtual* or *logical addresses*
	- converted into physical addresses by combination of hardware and software actions
	- *Memory Management Unit* keeps track of which parts of the virtual address space are in main memory
	- *MMU* translates virtual address into physical address
## Address Translation
- all programs and data are composed of fixed-length units called *pages* (2K to 16K bytes)
- data hard to locate (large size) but can be transferred at a rate of several megabytes per second
- each virtual address is interpreted as a *virtual page number* followd by an *offset* (location of byte/word within page)
- location of pages kept in *page table* in memory
- page table includes memory location of *page frame* (location in main memory which stores a page) and status of page
- *page table base register* points to the starting address of the table
- status bit shows if page has been changed and needs to be stored in main memory before being replaced
### Translation Lookaside Buffer
- small portion of the table (most recently accessed pages) mantained inside MMU called TLB
- works the same as a memory and it's cache (virtuall address hit and misses)
## Page Faults
- *page fault*: program generates an access request to a page that is not in the main memory
- processing of program is interrupted by MMU 
- other program is executed while page is fetched from disk into main memory
- Two options to ensure the interrupted program continues correctly: continue from the point of interruption or restart the instruction
- Choosing which page to remove is critical when a new page is brought from the disk
	- LRU replacement algorithm can be applied to page replacement
	- Control bits in page table entries can be used to record usage history
- Modified page has to be written back to disk before being removed from main memory
	- Write-through protocol is not suitable for virtual memory since writing small changes takes too long
- Looking up entries in the TLB introduces delay
- Keeping recently used TLB entries in special registers can reduce address translation time

---
References: