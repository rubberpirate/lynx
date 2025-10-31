# Lynx - .NET Reactor Reverse Engineering Challenge

## 🎯 Overview

`lynx.exe` is a Windows GUI application protected with .NET Reactor obfuscation. The challenge involves bypassing the protection to extract the hidden password validation logic.

**Target Details:**
- Platform: Windows x64
- Language: .NET Framework
- Protection: .NET Reactor
- Size: 187KB
- Interface: Simple password input form

## 📖 Full Writeup

For a detailed walkthrough of the reverse engineering process, check out the complete writeup:
[Cracking a .NET Reactor Protected Executable](https://medium.com/@rubberpirate/cracking-a-net-reactor-protected-executable-a-reverse-engineering-challenge-73248c55fb8b)

## 🛠️ Required Tools

### 1. **dnSpy** - .NET Decompiler & Debugger
- **Purpose:** Static analysis and decompilation of .NET assemblies
- **Download:** [github.com/dnSpy/dnSpy](https://github.com/dnSpy/dnSpy)
- **Usage:** Initial analysis and final decompilation of dumped assembly

### 2. **Detect It Easy (DIE)** - Packer/Protector Detection
- **Purpose:** Identify protection schemes and packers
- **Download:** [github.com/horsicq/Detect-It-Easy](https://github.com/horsicq/Detect-It-Easy)
- **Usage:** Detect .NET Reactor protection

### 3. **MegaDumper** - .NET Memory Dumper
- **Purpose:** Basic .NET assembly dumping from memory
- **Download:** [github.com/CodeCracker-Tools/MegaDumper](https://github.com/CodeCracker-Tools/MegaDumper)
- **Note:** May not work on heavily protected executables

### 4. **ExtremeDumper** - Advanced .NET Memory Dumper
- **Purpose:** Advanced memory dumping for heavily protected .NET apps
- **Download:** [github.com/wwh1004/ExtremeDumper](https://github.com/wwh1004/ExtremeDumper)
- **Important:** Use the 32-bit (x86) version for 32-bit targets!

## 🔍 Methodology

### Step 1: Static Analysis
```bash
# Open lynx.exe in dnSpy
# Expected result: No visible managed code (protected)
```

### Step 2: Protection Detection
```bash
# Run Detect It Easy on lynx.exe
# Result: .NET Reactor protection identified
```

### Step 3: Attempt Basic Memory Dump
```bash
# Run lynx.exe
# Launch MegaDumper
# Attach to lynx.exe process
# Expected result: May fail due to advanced protection
```

### Step 4: Advanced Memory Dump
```bash
# Run lynx.exe
# Launch ExtremeDumper (32-bit version)
# Attach to lynx.exe process
# Dump all modules
# Result: CrackBee.exe and supporting DLLs extracted
```

### Step 5: Final Analysis
```bash
# Open CrackBee.exe in dnSpy
# Navigate to Form1 → checkBtn_Click method
# Extract password validation logic
```

## 🏁 Solution

The password can be found by analyzing the dumped `CrackBee.exe` assembly in dnSpy. Look for the button click event handler that validates user input.

## 📚 Resources

- [Medium Writeup](https://medium.com/@rubberpirate/cracking-a-net-reactor-protected-executable-a-reverse-engineering-challenge-73248c55fb8b)
- [dnSpy Documentation](https://github.com/dnSpy/dnSpy)
- [ExtremeDumper Guide](https://github.com/wwh1004/ExtremeDumper)
