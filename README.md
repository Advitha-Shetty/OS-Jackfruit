# 🚀 Supervised Multi-Container Runtime

## 📌 Project Description

This project implements a lightweight container runtime in C using low-level Linux system calls. It demonstrates how containers work internally by building process isolation, logging, and kernel-level memory monitoring **without using Docker or external container tools**.

---

## ✨ Features

* Container creation using `clone()`
* Namespace isolation (PID, UTS, Mount)
* Filesystem isolation using `chroot()`
* Supervisor-client architecture using UNIX domain sockets
* Concurrent logging system using Producer-Consumer model (threads)
* Kernel module integration for memory monitoring
* CLI commands supported:

  * `start`
  * `run`
  * `stop`
  * `ps`
  * `logs`

---

## 🏗️ Architecture

```
Client → UNIX Domain Socket → Supervisor → Container
```

* Supervisor manages all containers
* Each container runs in isolated namespaces
* Logging handled via producer-consumer threads
* Kernel module monitors container memory usage

---

## 🛠️ Tech Stack

* **Language:** C
* **Operating System:** Linux (Ubuntu)
* **System Calls:** `clone`, `chroot`, `mount`
* **IPC:** UNIX domain sockets, pipes
* **Concurrency:** POSIX Threads (`pthread`)
* **Kernel Integration:** `ioctl`-based communication

---

## 📂 Project Structure

```
boilerplate/
├── engine.c              # Supervisor & runtime
├── monitor.c             # Kernel module
├── monitor_ioctl.h       # Shared definitions
├── Makefile              # Build automation
├── rootfs-base/          # Base filesystem
├── rootfs-alpha/         # Container filesystem
├── logs/                 # Log files
```

---

## ⚙️ Setup Instructions

### 1️⃣ Clone Repository

```bash
git clone https://github.com/<your-username>/OS-Jackfruit.git
cd OS-Jackfruit/boilerplate
```

### 2️⃣ Build Project

```bash
make clean
make
```

### 3️⃣ Load Kernel Module

```bash
sudo insmod monitor.ko
```

### 4️⃣ Start Supervisor

```bash
sudo ./engine supervisor ../rootfs-base
```

---

## 🚀 Usage

### 🔹 Start Container (Background)

```bash
sudo ./engine start c1 ../rootfs-alpha "/bin/sh"
```

### 🔹 Run Container (Blocking)

```bash
sudo ./engine run c2 ../rootfs-alpha "ls"
```

### 🔹 List Containers

```bash
sudo ./engine ps
```

### 🔹 View Logs

```bash
sudo ./engine logs c1
```

### 🔹 Stop Container

```bash
sudo ./engine stop c1
```

---

## 📊 Sample Output

```
Started container 'c1' pid=36577

ID               PID      STATE      STARTED              SOFT(MiB)  HARD(MiB)
c1               36577    running    2026-04-16 11:06:40  40         64
```

---

## 📚 Learning Outcomes

* Understanding Linux namespaces and process isolation
* Implementing IPC using sockets and pipes
* Designing concurrent systems using threads
* Integrating user-space programs with kernel modules
* Managing container lifecycle and resources

---

## 🔮 Future Improvements

* Add network namespace support
* Implement CPU resource limits
* Build a web-based monitoring dashboard
* Add container image support

---

## 👩‍💻 Authors

* Khushi Gupta
* Advitha D Shetty

---

## 📜 License

This project is developed for educational purposes.
