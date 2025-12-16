originally written by me, but corrected and edited with ai

## When to Use Assembly (Usermode)

### Performance-Critical
- Functions called thousands of times per frame
- Bone calculations, entity loops
- Microseconds matter for detection/performance

### Direct Memory Manipulation
- Custom memory patches (exact byte sequences)
- Trampolines and hooks (specific instruction layouts)
- Working around DEP/page protections

### Anti-Detection
- **Syscalls** - bypass user-mode hooks with direct `syscall` instruction
- **PEB walking** - hide modules manually
- **Custom calling conventions** - avoid normal patterns
- **Instruction obfuscation** - what compilers won't generate

### Hooking & Code Caves
- Minimal-size hooks (5-byte jumps, inline hooks)
- Preserve exact register states
- Position-independent shellcode
- Seamless execution returns

### Game Interfacing
- Non-standard calling conventions
- Exact stack layouts
- Functions using inline assembly

**Rule of thumb:** C/C++ for 95% of logic, assembly for <5% hotspots

---

## Kernel Driver Assembly Use

### System Operations
- SSDT hooks, custom syscall handlers
- Context switches (user/kernel mode)
- Register preservation

### Hardware Access
- **CR3 register** - process context switching
- **MSR manipulation** - hiding hooks
- **CPU instructions** - INVD, WBINVD

### Stealth
- IDT/GDT manipulation
- Inline kernel hooks (minimal footprint)
- PatchGuard bypasses
- EPT manipulation (hypervisor cheats)

### Critical Operations
- IRQL raising/lowering with precise timing
- Interrupt handling
- DPC manipulation

**Rule of thumb:** Kernel drivers are 95%+ C/C++, assembly for hardware-level control only

---

## Kernel Cheat Architecture

### Components
```
┌─────────────────────┐
│   Usermode Client   │ ← Game-specific (offsets, ESP, aimbot)
└──────────┬──────────┘
           │ (IOCTL / Shared Memory)
┌──────────▼──────────┐
│   Kernel Driver     │ ← General-purpose (R/W memory, stealth)
└─────────────────────┘
```

### Driver Types

**General-Purpose** (most common)
- Read/write arbitrary memory
- Query process/module info
- Hide from detection
- Bypass handle access checks
- Works for ALL games

**Game-Specific**
- Rare, unnecessary
- Driver doesn't need game knowledge

### What Goes Where

**Kernel Driver (General)**
- Memory primitives (read/write)
- Protection bypasses
- Stealth (hiding self)
- System-level hooks

**Usermode Client (Game-Specific)**
- Game offsets (EntityList, LocalPlayer, etc.)
- Game structures parsing
- ESP/aimbot logic
- Overlay rendering

---

## Why Kernel Drivers?

### Privilege Escalation
- Anticheats run in kernel (Ring 0)
- Usermode cheats (Ring 3) easily detected
- Driver operates at same level as AC

### Bypass Capabilities
- Read memory without handles (AC monitors handles)
- Hide from memory scans
- Hook/unhook AC functions
- Operate invisibly

---

## Driver Categories

### 1. Simple R/W Driver
- Exposes memory read/write only
- Cheat logic stays usermode
- **Pros:** Easy to code
- **Cons:** More detectable

### 2. Callback-Based
- Registers kernel callbacks (process notify, thread notify)
- Intercepts AC behavior
- **Pros:** Stealthier
- **Cons:** More complex

### 3. Hypervisor-Based
- Loads thin hypervisor (VT-x)
- Operates Ring -1 (below kernel)
- **Pros:** Hides from everything
- **Cons:** Hardest to develop

---

## Driver Signing Problem

**Windows requires signed drivers**

### Solutions
1. **Vulnerable driver exploit** (most common)
   - Load known vulnerable signed driver
   - Exploit it to map unsigned driver
   - Example: kdmapper

2. **Stolen certificates**
   - Use leaked signing cert
   - Works until cert revoked

3. **DSE bypass**
   - Disable Driver Signature Enforcement
   - Gets patched frequently

4. **Test signing mode**
   - Only for development
   - Doesn't work against real AC

---

## Real-World Example

```
kdmapper (exploit loader)
    ↓
Custom kernel driver (general R/W + stealth)
    ↓
CS2 usermode client (CS2 offsets + ESP)
    OR
Valorant usermode client (Valorant offsets + aimbot)
    OR
Apex usermode client (Apex offsets + triggerbot)
```

**Same driver, different game clients**

---

## Key info

- Assembly: Use sparingly, only when necessary  
- Kernel drivers: General-purpose, not game-specific  
- Usermode clients: Game-specific logic  
- Architecture: Driver = toolbox, Client = tool user  
- Signing: Biggest hurdle, multiple exploit methods exist