# Day 06 – Linux Fundamentals: Read & Write Text Files

## Objective
Practice basic Linux file input/output operations such as creating files, writing text, appending content, and reading file contents.

---

## 1. Create an Empty File

**Command**

```bash
touch notes.txt
```

**Explanation**

Creates an empty file named `notes.txt` if it does not already exist.

---

## 2. Write Text to the File (Overwrite)

**Command**

```bash
echo "Learning Linux file handling." > notes.txt
```

**Explanation**

Writes text into the file.  
The `>` operator creates the file if it doesn't exist or overwrites the existing content.

---

## 3. Append Text to the File

**Command**

```bash
echo "learning linux is important for devops" >> notes.txt
```

**Explanation**

Appends a new line to the file without removing existing content.

---

## 4. Write and Display Using tee

**Command**

```bash
echo "I'm enjoying learning Devops" | tee -a notes.txt
```

**Explanation**

The `tee` command writes the output to the file and displays it in the terminal at the same time.  
The `-a` flag appends the content to the file.

---

## 5. Read the Entire File

**Command**

```bash
cat notes.txt
```

**Explanation**

Displays the complete contents of the file.

---

## 6. Read the First Two Lines

**Command**

```bash
head -n 2 notes.txt
```

**Explanation**

Displays the first two lines of the file.

---

## 7. Read the Last Two Lines

**Command**

```bash
tail -n 2 notes.txt
```

**Explanation**

Displays the last two lines of the file.

---

## Final File Content

```
Learning Linux file handling.
Redirection helps write data into files.
Logs and configuration files are text files.
```

---

## Key Learning

- `touch` is used to create a file.
- `>` overwrites file content.
- `>>` appends content to an existing file.
- `tee` writes output to a file while also displaying it in the terminal.
- `cat`, `head`, and `tail` are useful for quickly reading file contents.

These commands are commonly used in DevOps for working with **logs, configuration files, and scripts**.
