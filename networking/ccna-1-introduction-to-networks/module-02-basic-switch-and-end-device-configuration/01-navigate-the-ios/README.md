# Lab 01 — Navigate the IOS

<img width="1439" height="899" alt="image" src="https://github.com/user-attachments/assets/9589dac9-017c-41d2-a113-640cca7e0a85" />

## Overview

This Packet Tracer lab introduced Cisco IOS navigation, command syntax verification, context-sensitive help, command completion, EXEC modes, and basic system clock configuration.

## Objectives

* Access the Cisco IOS CLI
* Navigate User EXEC, Privileged EXEC, and Global Configuration modes
* Use context-sensitive help (`?`)
* Use command completion (`Tab`)
* Interpret IOS command output and error messages
* Configure and verify the system clock

---

## Lab Results

### Part 1 — CLI Access and Help

**What is the bits per second setting?**

```text
9600
```

**What prompt is displayed after pressing ENTER?**

```text
S1>
```

**Which command begins with the letter `C`?**

```text
connect
```

**What commands are displayed with `t?`?**

```text
telnet
terminal
traceroute
```

**What commands are displayed with `te?`?**

```text
telnet
terminal
```

---

### Part 2 — EXEC Modes

**What information is displayed for the `enable` command?**

```text
Turn on privileged commands
```

**What is displayed after pressing `Tab` on `en`?**

```text
enable
```

**What happens when entering `te<Tab>`?**

The command is not completed because multiple commands begin with `te`.

**How does the prompt change after `enable`?**

```text
S1>  →  S1#
```

**How many commands beginning with `C` are available in Privileged EXEC mode?**

```text
clock
clear
configure
connect
copy
```

**What message is displayed after `configure`?**

```text
Configuring from terminal, memory, or network [terminal]?
```

**How does the prompt change after entering Global Configuration Mode?**

```text
S1#  →  S1(config)#
```

---

## Clock Configuration

### Initial Clock Verification

The initial system clock was checked using:

```text
S1# show clock
```

The switch displayed its default clock values.

### Configure Clock

Context-sensitive help was used to determine the correct syntax:

```text
S1# clock ?
S1# clock set ?
```

The system clock was then configured as required by the lab:

```text
S1# clock set 15:00:00 31 january 2035
```

### Verification

The configuration was verified with:

```text
S1# show clock
```

Output:

```text
15:0:23.257 UTC Wed Jan 31 2035
```

✅ **Clock successfully configured.**

<img width="1439" height="899" alt="image" src="https://github.com/user-attachments/assets/def08c1e-99a9-4307-b610-e896cbd201cb" />

---

## IOS Messages Explored

### Command Completion

Using `Tab` completed an unambiguous command:

```text
S1# cl<Tab>
```

Result:

```text
clock
```

### Incomplete Command

Entering an incomplete command produced:

```text
S1# clock

% Incomplete command.
```

### Context-Sensitive Help

The `?` operator displayed the available subcommand:

```text
S1# clock ?

set  Set the time and date
```

### Time Parameter Request

Further help displayed the required time format:

```text
S1# clock set ?

hh:mm:ss  Current Time
```

### Invalid Values

IOS rejected invalid time values:

```text
S1# clock set 25:00:00

% Invalid input detected
```

An invalid day was also rejected:

```text
S1# clock set 15:00:00 32

% Invalid input detected
```

---

## Key Takeaways

* Distinguished between User EXEC, Privileged EXEC, and Global Configuration modes.
* Used context-sensitive help (`?`) to discover IOS commands and syntax.
* Used command completion with the `Tab` key.
* Interpreted incomplete-command and invalid-input messages.
* Configured the Cisco IOS system clock.
* Verified the configuration using `show clock`.
* Practiced navigating and troubleshooting the Cisco IOS CLI.
