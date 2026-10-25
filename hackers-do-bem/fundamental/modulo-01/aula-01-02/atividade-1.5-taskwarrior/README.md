# Activity 1.5 — Task Management with Taskwarrior

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 01  
> **Class:** 01–02  
> **Environment:** Kali Linux  
> **Status:** Completed

## Objective

Practice command-line task management using Taskwarrior by creating tasks, adding tags, setting due dates, and marking tasks as completed.

## Environment

- **Operating system:** Kali Linux
- **Terminal:** Linux command line
- **Tool:** Taskwarrior
- **Configuration directory:** `~/.task`
- **Configuration file:** `~/.taskrc`

## Procedure

### 1. Configure Taskwarrior

The terminal was opened in an administrator shell, and the directory used by Taskwarrior was configured:

```bash
sudo -i
mkdir -p ~/.task
echo 'data.location=~/.task' > ~/.taskrc
```

The `data.location` setting specifies where Taskwarrior stores its task data. The `~/.taskrc` file contains the configuration setting, while `~/.task` is the designated data directory.

**Note:** Because the setup was performed after `sudo -i`, the configuration and task data belong to the `root` user. Root privileges are not normally required for task management; using a regular user account is preferable for routine operations.

### 2. Create Tasks

Three tasks were created using the following commands:

```bash
task add Comprar leite
task add Comprar cafe
task add Comprar salgados
```

The `task list` command was then used to display the tasks:

```bash
task list
```

Taskwarrior assigned numeric identifiers to the new tasks. These identifiers were used in subsequent operations.

The task descriptions were kept in Portuguese to match the original laboratory procedure.

### 3. Add an Urgency Tag

The task with ID `2` was modified to include the `urgent` tag:

```bash
task 2 modify +urgent
```

The task list was then displayed again:

```bash
task list
```

The `+urgent` syntax adds a tag named `urgent` to the task. Tags can help categorize and filter tasks, but this command does not set Taskwarrior's priority attribute.

### 4. Set a Due Date

A due date was assigned to task `3`:

```bash
task 3 modify due:2036-12-31
```

The task list was displayed again:

```bash
task list
```

Task `3` now had a due date of December 31, 2036.

### 5. Mark a Task as Completed

Task `1` was marked as completed:

```bash
task 1 done
```

Finally, the task list was checked again:

```bash
task list
```

The completed task no longer appeared among the pending tasks in the default list report.

## Commands Used

```bash
sudo -i
mkdir -p ~/.task
echo 'data.location=~/.task' > ~/.taskrc

task add Comprar leite
task add Comprar cafe
task add Comprar salgados

task list

task 2 modify +urgent
task list

task 3 modify due:2036-12-31
task list

task 1 done
task list
```

## Result

The activity demonstrated how to manage tasks from the Linux command line using Taskwarrior.

The following operations were performed:

- Created three tasks.
- Listed the tasks and identified their numeric IDs.
- Added the `urgent` tag to a task.
- Assigned a due date to another task.
- Marked a task as completed.

## Concepts Practiced

- Command-line task management
- Taskwarrior configuration
- Task creation and listing
- Task identifiers
- Tags and task categorization
- Due dates and deadlines
- Task completion and status management
- Linux terminal operations

## Evidence

The activity evidence is included in the PDF for Classes 01–02.

[View Evidence — Classes 01–02](../evidencias.pdf)

---

[Back to Classes 01–02](../) · [Back to Module 01](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
