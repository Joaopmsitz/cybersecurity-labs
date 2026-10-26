# Activity 6.01 — Code Reuse in Python on Kali Linux

> **Program:** Hackers do Bem  
> **Stage:** Fundamental — Module 06  
> **Class:** 21–22  
> **Environment:** Kali Linux  
> **Status:** Completed

## Objective

This activity demonstrates the concept of code reuse in Python using the Pillow library to process an image.

The exercise involves downloading an image to Kali Linux, using Python code based on an existing library to resize it to 300 × 300 pixels, and saving the result to a new file.

The objective is to understand how previously developed and tested software components can be reused to implement functionality without having to develop all the image-processing logic from scratch.

## Environment

- **Operating system:** Kali Linux
- **Access method:** RDP
- **Machine IP address:** `192.168.98.40`
- **User:** `aluno`
- **Working directory:** `/home/aluno/Documentos/`

The credentials used in the laboratory are not recorded in this document.

## Procedure

### 1. Prepare the Environment

Before beginning the module activities, cached APT files, packages that were no longer needed, and old logs were cleaned up according to the laboratory instructions:

```bash
sudo apt clean
sudo apt autoremove
sudo journalctl --vacuum-time=1d
```

These commands are intended to free up space on the virtual machine before the activities are performed.

### 2. Open the Terminal

After accessing Kali Linux through RDP, the terminal was opened, and administrative access was obtained:

```bash
sudo -i
```

The Documents directory was then accessed:

```bash
cd /home/aluno/Documentos
```

An initial check of the directory contents was performed:

```bash
ls
```

### 3. Download the Image

The image `My_shoe.jpg` was downloaded directly from the terminal using `wget`:

```bash
wget https://upload.wikimedia.org/wikipedia/commons/0/01/My_shoe.jpg
```

**Output recorded in the laboratory material:**

```text
--2024-02-13 17:24:33--  https://upload.wikimedia.org/wikipedia/commons/0/01/My_shoe.jpg
Resolvendo upload.wikimedia.org (upload.wikimedia.org)... 208.80.154.240, 2620:0:861:ed1a::2:b
Conectando-se a upload.wikimedia.org (upload.wikimedia.org)|208.80.154.240|:443... conectado.
A requisição HTTP foi enviada, aguardando resposta... 200 OK
Tamanho: 1297035 (1,2M) [image/jpeg]
Salvando em: “My_shoe.jpg”

My_shoe.jpg                 100%[==========================================>]   1,24M  --.-KB/s    em 0,1s    

2024-02-13 17:24:33 (8,28 MB/s) - “My_shoe.jpg” salvo [1297035/1297035]
```

After the download, the following command was executed:

```bash
ls
```

**Result:**

```text
My_shoe.jpg
```

This confirms that the image was stored in `/home/aluno/Documentos`.

### 4. View the Original Image

With the file available on the system, Thunar, the Kali Linux file manager, was opened.

Navigation was performed to:

```text
/home/aluno/Documentos
```

The `My_shoe.jpg` file was opened to view the original image.

After viewing it, the image viewer was closed.

### 5. Create the Python Script

The Mousepad text editor was opened, and the following code was entered:

```python
from PIL import Image

# Open an existing image
imagem_original = Image.open("My_shoe.jpg")

# Resize the image to 300x300 pixels
imagem_redimensionada = imagem_original.resize((300, 300))

# Save the resized image
imagem_redimensionada.save("My_shoe_redimensionado.jpg")

# Close the original image
imagem_original.close()
```

The code uses the Pillow library, which provides image-manipulation functionality in Python.

#### Import the Library

```python
from PIL import Image
```

This imports the `Image` class from the Pillow library.

It provides methods for operations such as opening, resizing, and saving images.

#### Open the Image

```python
imagem_original = Image.open("My_shoe.jpg")
```

The `Image.open()` function opens the existing image and assigns the resulting object to the `imagem_original` variable.

#### Resize the Image

```python
imagem_redimensionada = imagem_original.resize((300, 300))
```

The `resize()` method creates a new version of the image with the following dimensions:

```text
300 x 300 pixels
```

The result is stored in `imagem_redimensionada`.

**Note:** Resizing directly to 300 × 300 pixels can change the original image's aspect ratio if its proportions differ from a square.

#### Save the Image

```python
imagem_redimensionada.save("My_shoe_redimensionado.jpg")
```

The resized image is saved under the following filename:

```text
My_shoe_redimensionado.jpg
```

#### Close the Original Image

```python
imagem_original.close()
```

This closes the original image file after it has been used.

Closing resources when they are no longer needed is good practice and helps avoid keeping files or resources open unnecessarily.

### 6. Save the Script

The code was saved in the following directory:

```text
/home/aluno/Documentos
```

using the filename:

```text
redimensionar_imagem.py
```

In Mousepad, the **All Files** option had to be selected when saving so that the file would be created with the `.py` extension.

### 7. Execute the Program

After closing Mousepad, the terminal was used to execute the script:

```bash
python redimensionar_imagem.py
```

The script uses the original image as input and generates a new resized image.

### 8. Verify the Generated Files

After the program executed, the following command was used:

```bash
ls
```

**Expected output in the laboratory:**

```text
My_shoe.jpg  My_shoe_redimensionado.jpg  redimensionar_imagem.py
```

The output shows that three files are present in the directory:

```text
My_shoe.jpg
My_shoe_redimensionado.jpg
redimensionar_imagem.py
```

The additional file, `My_shoe_redimensionado.jpg`, confirms that the Python script performed the image-processing operation and created a new file.

This is the step specified for the activity evidence.

## Concepts Practiced

### Code Reuse

The main concept demonstrated in this activity is code reuse.

Instead of manually implementing all the logic required to interpret a JPEG file, manipulate pixels, and generate a new image, the program uses functionality provided by the Pillow library.

The relationship can be represented as follows:

```text
Python
   │
   ▼
Pillow Library
   │
   ├── Open image
   ├── Resize image
   └── Save image
```

In this way, previously developed components can be incorporated into new programs, reducing the amount of code required and allowing developers to focus on the application's specific logic.

### Pillow Library

Pillow is a Python library that provides tools for image processing.

In this activity, it was used to open an existing image, resize it, and save the result as a new JPEG file.

### Python Script Execution

The command:

```bash
python redimensionar_imagem.py
```

runs the Python script from the terminal.

The script performs the operations defined in the source code using the downloaded image as input.

## Results

The activity demonstrated the practical reuse of a Python library for image processing.

The workflow was:

```text
Download My_shoe.jpg
        ↓
Open image with Pillow
        ↓
Resize to 300 x 300
        ↓
Save My_shoe_redimensionado.jpg
        ↓
Verify the generated file
```

The `My_shoe_redimensionado.jpg` file was generated from the original image using the `redimensionar_imagem.py` script.

## Laboratory Cleanup

After completing the activity, the files used were removed from the Documents directory:

```bash
rm *
```

The laboratory requested confirmation before removing the files:

```text
zsh: sure you want to delete all 3 files in /home/aluno/Documentos [yn]? y
```

The following command was then used to verify the final directory contents:

```bash
ls
```

**Warning:** The `rm *` command is destructive and removes all files matching the pattern in the current directory. In a real environment, it is safer to inspect the directory contents beforehand and remove only the files that need to be deleted.

## Evidence

The evidence for this activity corresponds to Step 8, showing the file listing after the script was executed:

```text
My_shoe.jpg  My_shoe_redimensionado.jpg  redimensionar_imagem.py
```

[View Evidence — Classes 21–22](../evidencias.pdf)

---

[Back to Classes 21–22](../) · [Back to Module 06](../../README.md) · [Back to Fundamental](../../../README.md) · [Back to Hackers do Bem](../../../../README.md)
