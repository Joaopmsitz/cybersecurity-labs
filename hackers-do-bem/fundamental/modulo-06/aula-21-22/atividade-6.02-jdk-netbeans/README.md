# Activity 6.02 — Exploring the Java Development Kit (JDK) and an IDE on Kali Linux

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 06  
> **Class:** 21–22  
> **Environment:** Kali Linux  
> **Status:** Completed

## Objective

This activity covers the installation and verification of the Java development environment on Kali Linux using the Java Development Kit (JDK) and Apache NetBeans as the IDE.

The exercise demonstrates the relationship between the JDK, which provides tools required for Java development, and an IDE, which provides an integrated environment for creating and developing applications.

## Environment

- **Operating system:** Kali Linux
- **Access method:** RDP
- **Machine IP address:** `192.168.98.40`
- **User:** `aluno`
- **NetBeans directory:** `/curso/netbeans`

The credentials used in the laboratory are not recorded in this document.

## Procedure

### 1. Open the Terminal

After accessing Kali Linux through RDP, the terminal was opened, and administrative access was obtained:

```bash
sudo -i
```

Administrative access was used to inspect and install the Apache NetBeans package.

### 2. Check the JDK

The laboratory already provided an installed JDK. To check the available Java version, the following command was executed:

```bash
java --version
```

**Observed output:**

```text
openjdk 23-ea 2024-09-17
OpenJDK Runtime Environment (build 23-ea+20-Debian-1)
OpenJDK 64-Bit Server VM (build 23-ea+20-Debian-1, mixed mode, sharing)
```

The output confirms that an OpenJDK version was available in the environment.

#### OpenJDK

OpenJDK is an open-source implementation of the Java platform.

The JDK provides components required for Java development, including tools used to compile and run applications.

The version reported in the laboratory was:

```text
OpenJDK 23-ea
```

**Technical note:** The `java --version` command confirms that the Java runtime is available. To verify the Java compiler specifically, the `javac --version` command can also be used.

### 3. Access the NetBeans Directory

The Apache NetBeans package used in the activity was stored in the following directory:

```text
/curso/netbeans
```

The directory was accessed using:

```bash
cd /curso/netbeans
```

### 4. Check the Installation Package

After entering the directory, the following command was executed:

```bash
ls
```

**Observed output:**

```text
apache-netbeans_19-1_all.deb
```

The `.deb` file is the package used to install Apache NetBeans on the system.

The `.deb` format is used by Debian-based distributions, including Kali Linux.

### 5. Install Apache NetBeans

The installation was performed using `dpkg`:

```bash
dpkg -i apache-netbeans_19-1_all.deb
```

**Observed output:**

```text
Selecionando pacote previamente não selecionado apache-netbeans.
(Lendo banco de dados ... 364754 arquivos e diretórios atualmente instalados).
Preparando para desempacotar apache-netbeans_19-1_all.deb ...
Desempacotando apache-netbeans (19-1) ...
Configurando apache-netbeans (19-1) ...
Processando gatilhos para kali-menu (2025.3.2) ...
Processando gatilhos para desktop-file-utils (0.28-1) ...
Processando gatilhos para hicolor-icon-theme (0.18-2) ...
```

The output indicates the main stages performed by `dpkg`:

- Identifying the package.
- Preparing the package for installation.
- Unpacking the files.
- Configuring Apache NetBeans.
- Processing triggers related to the Kali menu.
- Updating desktop files.
- Processing the system icon theme.

### 6. Open Apache NetBeans

After installation, Apache NetBeans was launched through the Kali Linux application menu:

```text
Aplicativos
└── Aplicativos habituais
    └── Desenvolvimento
        └── Apache NetBeans
```

The application was opened to verify that the IDE was available and could be launched.

### 7. Explore NetBeans

With Apache NetBeans open, the integrated development environment was displayed.

NetBeans is an IDE (Integrated Development Environment).

An IDE combines tools that support software development in one application, including:

- Code editing.
- Project organization.
- Application execution.
- Debugging.
- File management.
- Integration with development tools.

This is the step specified for the activity evidence.

## Concepts Practiced

### JDK — Java Development Kit

The JDK is the development kit used to create Java applications.

It provides tools required to work with the Java ecosystem, including components used to compile and run programs.

In this activity, Java availability was checked using:

```bash
java --version
```

The reported result was:

```text
openjdk 23-ea 2024-09-17
```

### IDE — Integrated Development Environment

An IDE provides an integrated environment for software development.

Instead of using separate tools to edit, execute, and organize code, developers can perform these tasks within a single application.

### Apache NetBeans

Apache NetBeans is an IDE that supports application development, including Java projects.

In this activity, it was installed using the package:

```text
apache-netbeans_19-1_all.deb
```

The installation command was:

```bash
dpkg -i apache-netbeans_19-1_all.deb
```

### `dpkg`

`dpkg` is a low-level tool used to install, remove, and manage `.deb` packages on Debian-based systems.

In this activity, it was used to install the local Apache NetBeans package:

```bash
dpkg -i apache-netbeans_19-1_all.deb
```

### Relationship Between the JDK and an IDE

The JDK and NetBeans have different but complementary roles:

```text
JDK
 │
 ├── Java platform tools
 ├── Compilation
 └── Execution
       │
       ▼
Apache NetBeans
 │
 ├── Editor
 ├── Projects
 ├── Execution
 └── Development tools
```

The JDK provides the underlying tools needed to work with Java, while the IDE provides an integrated interface to facilitate development.

## Results

The activity confirmed that Java was available on Kali Linux and installed Apache NetBeans using a `.deb` package.

Java availability was checked with:

```bash
java --version
```

The NetBeans package was installed using:

```bash
dpkg -i apache-netbeans_19-1_all.deb
```

After installation, Apache NetBeans was opened and explored, confirming that the IDE was available in the system.

## Evidence

The evidence for this activity corresponds to Step 7, showing Apache NetBeans open after installation and displaying the IDE interface.

[View Evidence — Classes 21–22](../evidencias.pdf)

---

[Back to Classes 21–22](../) · [Back to Module 06](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
