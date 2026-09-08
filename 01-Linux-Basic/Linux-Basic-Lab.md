# Linux Basic Lab – Ubuntu Server 24.04

> **Mục tiêu:** Làm quen với môi trường Linux/Ubuntu Server, Terminal, Shell và Linux Filesystem thông qua thực hành trực tiếp trên máy Ubuntu Server 24.04.

---

## 1. Thông tin môi trường thực hành

Các lệnh được thực hiện trực tiếp trên Ubuntu Server.

| Thành phần | Kết quả |
|---|---|
| User | `tungdd` |
| Hostname | `ubuntuserver2404` |
| Operating System | Ubuntu 24.04.4 LTS |
| Codename | Noble Numbat (`noble`) |
| Kernel | `6.8.0-139-generic` |
| Architecture | `x86_64` |
| Shell | `/bin/bash` |
| Home Directory | `/home/tungdd` |

---

# 2. Linux Basic

## 2.1. Kiểm tra user hiện tại

### Command

```bash
whoami
```

### Kết quả thực tế

```text
tungdd
```

### Nhận xét

Lệnh `whoami` cho biết user hiện tại đang đăng nhập và thực thi các câu lệnh trên hệ thống.

## 2.2. Kiểm tra thư mục hiện tại

### Command

```bash
pwd
```

### Kết quả thực tế

```text
/home/tungdd
```

### Nhận xét

`pwd` là viết tắt của **Print Working Directory**, dùng để xác định vị trí hiện tại trong Linux Filesystem.

Thư mục `/home/tungdd` là Home Directory của user `tungdd`.

---

## 2.3. Liệt kê nội dung thư mục

### Command

```bash
ls
```

### Kết quả

Tại thời điểm thực hành, thư mục Home không có nội dung hiển thị bằng lệnh `ls`.

### Nhận xét

`ls` dùng để liệt kê file và directory trong thư mục hiện tại.

Để xem cả file ẩn và thông tin chi tiết có thể sử dụng:

```bash
ls -la
```

---

# 3. Kiểm tra hệ điều hành và Kernel

## 3.1. Kiểm tra Kernel

### Command

```bash
uname -a
```

### Kết quả thực tế

```text
Linux ubuntu 6.8.0-139-generic #139-Ubuntu SMP PREEMPT_DYNAMIC Sat Aug 1 03:52:05 UTC 2026 x86_64 x86_64 x86_64 GNU/Linux
```

### Phân tích

Một số thông tin quan trọng:

- `Linux`: Linux Kernel đang được sử dụng.
- `6.8.0-139-generic`: phiên bản Kernel.
- `x86_64`: kiến trúc hệ thống 64-bit.
- `GNU/Linux`: môi trường Linux sử dụng GNU utilities.

### Ý nghĩa đối với DevOps

Kernel là thành phần cốt lõi nằm giữa phần cứng và các chương trình chạy trên hệ điều hành.

Hiểu thông tin Kernel giúp xác định môi trường khi troubleshooting, kiểm tra compatibility và quản trị server.

---

# 4. Ubuntu Server 24.04

## 4.1. Kiểm tra phiên bản Ubuntu

### Command

```bash
cat /etc/os-release
```

### Kết quả thực tế

```text
PRETTY_NAME="Ubuntu 24.04.4 LTS"
NAME="Ubuntu"
VERSION_ID="24.04"
VERSION="24.04.4 LTS (Noble Numbat)"
VERSION_CODENAME=noble
ID=ubuntu
ID_LIKE=debian
```

### Nhận xét

Máy thực hành đang sử dụng:

**Ubuntu 24.04.4 LTS – Noble Numbat**

`VERSION_ID="24.04"` xác định dòng Ubuntu 24.04.

Ubuntu thuộc họ Debian, thể hiện qua:

```text
ID_LIKE=debian
```

Điều này cũng liên quan đến việc sử dụng hệ thống quản lý package `apt`.

---

# 5. Terminal và Shell

## 5.1. Kiểm tra Shell

### Command

```bash
echo $SHELL
```

### Kết quả thực tế

```text
/bin/bash
```

### Nhận xét

Shell hiện tại là **Bash**.

Có thể hình dung quá trình làm việc:

```text
User
  ↓
Terminal
  ↓
Bash Shell
  ↓
Linux Kernel
  ↓
Hardware
```

Terminal là giao diện để người dùng tương tác với hệ thống.

Shell là chương trình tiếp nhận và xử lý các câu lệnh người dùng nhập vào.

---

# 6. Linux Filesystem

## 6.1. Kiểm tra Root Directory

### Command

```bash
ls /
```

### Kết quả thực tế

Hệ thống hiển thị các thư mục chính như:

```text
bin
boot
dev
etc
home
lib
lib64
media
mnt
opt
proc
root
run
sbin
snap
srv
sys
tmp
usr
var
```

### Cấu trúc tổng quát

```text
/
├── bin
├── boot
├── dev
├── etc
├── home
│   └── tungdd
├── lib
├── lib64
├── media
├── mnt
├── opt
├── proc
├── root
├── run
├── sbin
├── snap
├── srv
├── sys
├── tmp
├── usr
└── var
```

`/` là **Root Directory**, tức thư mục gốc của Linux Filesystem.

> Lưu ý: `/` và `/root` là hai khái niệm khác nhau. `/` là thư mục gốc của toàn bộ filesystem, còn `/root` là Home Directory của user `root`.

---

# 7. Các thư mục quan trọng

## `/home`

Chứa Home Directory của các user thông thường.

Trong môi trường thực hành:

```text
/home/tungdd
```

là Home Directory của user `tungdd`.

---

## `/etc`

Chứa nhiều file cấu hình của hệ thống và các dịch vụ.

Ví dụ:

```text
/etc/os-release
/etc/ssh/
/etc/hosts
```

Trong bài thực hành, file:

```text
/etc/os-release
```

được sử dụng để kiểm tra phiên bản Ubuntu.

Đây là một thư mục đặc biệt quan trọng đối với Linux System Administration và DevOps.

---

## `/var`

Chứa dữ liệu thường xuyên thay đổi trong quá trình hệ thống và ứng dụng hoạt động.

Một khu vực quan trọng:

```text
/var/log
```

dùng để lưu nhiều loại log.

---

## `/var/log`

Trong bài thực hành đã kiểm tra:

```bash
ls -la /var/log | head
```

Một số nội dung quan sát được:

```text
alternatives.log
apparmor
auth.log
bootstrap.log
btmp
cloud-init.log
```

### Ý nghĩa

- `auth.log`: liên quan đến hoạt động xác thực.
- `cloud-init.log`: log của cloud-init, thường gặp trong quá trình khởi tạo server.
- Các log khác phục vụ việc theo dõi hoạt động của hệ thống và dịch vụ.

Phần Logs sẽ được tìm hiểu sâu hơn ở bài học sau.

---

## `/tmp`

Chứa các dữ liệu tạm thời của hệ thống và ứng dụng.

Không nên tùy tiện xóa toàn bộ nội dung `/tmp` khi chưa hiểu rõ tác động.

---

## `/usr`

Chứa nhiều chương trình, thư viện và dữ liệu phục vụ hệ thống.

Một số thư mục thường gặp:

```text
/usr/bin
/usr/sbin
/usr/lib
```

---

## `/opt`

Thường được sử dụng cho các phần mềm hoặc ứng dụng bổ sung được cài đặt theo cách riêng.

---

## `/boot`

Chứa các thành phần cần thiết cho quá trình boot hệ thống, bao gồm các file liên quan đến Linux Kernel và bootloader.

---

## `/dev`

Chứa các device files đại diện cho thiết bị và một số interface đặc biệt của hệ thống.

Ví dụ:

```text
/dev/null
/dev/random
```

---

## `/proc`

Filesystem đặc biệt cung cấp thông tin liên quan đến process và Kernel.

Ví dụ:

```bash
cat /proc/cpuinfo
cat /proc/meminfo
```

---

## `/sys`

Cung cấp interface và thông tin liên quan đến Kernel, thiết bị và hệ thống.

---

# 8. `ls -la` và thông tin file

Đã sử dụng:

```bash
ls -la /home/tungdd
```

Kết quả cho thấy các file/thư mục ẩn như:

```text
.bash_logout
.bashrc
.cache
.profile
.ssh
```

Ví dụ:

```text
-rw-r--r-- 1 tungdd tungdd 3771 ... .bashrc
```

Có thể nhận biết:

```text
-rw-r--r--   tungdd   tungdd
│            │        │
│            │        └── Group
│            └─────────── Owner
└──────────────────────── Permission
```

Phần Permission sẽ được học riêng sau File & Directory.

---

# 9. `df -h` – kiểm tra dung lượng Filesystem

### Command

```bash
df -h
```

Trong kết quả thực hành, filesystem chính được mount tại `/`:

```text
/dev/mapper/ubuntu--vg-ubuntu--lv
```

với thông tin quan sát được:

```text
Size   Used   Avail   Use%   Mounted on
9.8G   2.6G   6.7G    29%    /
```

### Nhận xét

- `Size`: tổng dung lượng filesystem.
- `Used`: dung lượng đã sử dụng.
- `Avail`: dung lượng còn khả dụng.
- `Use%`: phần trăm dung lượng đã sử dụng.
- `Mounted on`: vị trí filesystem được mount.

Máy cũng hiển thị các filesystem dạng `tmpfs`, được sử dụng cho một số vùng dữ liệu tạm thời trong hệ thống.

---

# 10. `du -sh` – kiểm tra dung lượng Directory

### Command

```bash
du -sh /home/tungdd
```

### Kết quả thực tế

```text
24K    /home/tungdd
```

### Phân tích

- `du`: Disk Usage.
- `-s`: Summary, chỉ hiển thị tổng.
- `-h`: Human-readable.

Kết quả cho thấy `/home/tungdd` đang sử dụng khoảng **24 KB** tại thời điểm thực hành.

---

# 11. Phân biệt `df` và `du`

Đây là kiến thức quan trọng khi quản trị Linux Server.

```text
df → Filesystem
du → File / Directory
```

### `df`

```bash
df -h
```

Trả lời câu hỏi:

> Filesystem còn bao nhiêu dung lượng?

### `du`

```bash
du -sh /home/tungdd
```

Trả lời câu hỏi:

> Directory hoặc file đang chiếm bao nhiêu dung lượng?

Trong thực tế DevOps, hai lệnh này rất hữu ích khi server có vấn đề **full disk**.

---

# 12. Tổng kết kiến thức đã thực hành

Đã thực hành và kiểm tra:

```text
Linux Basic
    ↓
Ubuntu Server 24.04       ✅
    ↓
Terminal                   ✅
    ↓
Shell / Bash               ✅
    ↓
Filesystem                 ✅
    ↓
File & Directory           ⏳
    ↓
Permission                 ⏳
    ↓
Process                    ⏳
    ↓
Package                    ⏳
    ↓
Service                    ⏳
    ↓
Network                    ⏳
    ↓
Logs                       ⏳
```

## Kiến thức đã nắm được

- Xác định user hiện tại bằng `whoami`.
- Xác định thư mục hiện tại bằng `pwd`.
- Liệt kê file và directory bằng `ls`.
- Kiểm tra Kernel bằng `uname`.
- Kiểm tra hostname bằng `hostname`.
- Kiểm tra phiên bản Ubuntu bằng `/etc/os-release`.
- Xác định Shell hiện tại bằng `$SHELL`.
- Hiểu `/` là Root Directory.
- Nhận biết vai trò cơ bản của `/home`, `/etc`, `/var`, `/var/log`, `/tmp`, `/usr`, `/opt`, `/boot`, `/dev`, `/proc`, `/sys`.
- Sử dụng `ls -la` để quan sát owner, group và permission.
- Kiểm tra dung lượng filesystem bằng `df -h`.
- Kiểm tra dung lượng directory bằng `du -sh`.
- Bắt đầu làm quen với cấu trúc Linux Server thực tế.

---

# 13. Nhận xét cá nhân

Qua bài thực hành, tôi hiểu rõ hơn cách Linux tổ chức hệ thống thay vì chỉ ghi nhớ các câu lệnh riêng lẻ.

Điểm quan trọng nhất tôi nhận thấy là khi làm DevOps cần có khả năng **quan sát hệ thống, đọc output và hiểu vị trí của dữ liệu/cấu hình/log**.

Ví dụ:

```text
/etc       → Configuration
/var/log   → Logs
/home      → User data
/proc      → Process / Kernel information
df         → Filesystem usage
du         → Directory/File usage
```

Đây là nền tảng để tiếp tục học **File & Directory → Permission → Process → Package → Service → Network → Logs**.

---

## 14. Minh chứng thực hành

Các kết quả trong báo cáo được lấy từ quá trình thực hành trực tiếp trên Ubuntu Server 24.04.

Có thể lưu ảnh chụp màn hình vào:

```text
01-Linux-Basic/
└── images/
```

và chèn vào Markdown, ví dụ:

```markdown
![Linux Basic Lab](../images/linux-basic-lab.png)
```

---

## 15. Kết luận

Bài thực hành đã giúp xây dựng nền tảng ban đầu về Linux và Ubuntu Server.

Thay vì chỉ học lý thuyết, các kiến thức được kiểm chứng bằng việc thực hiện trực tiếp các câu lệnh trên server và phân tích output thực tế.

**Bài tiếp theo: File & Directory.**


---

# 16. Ảnh minh chứng thực hành

Các ảnh dưới đây là **ảnh chụp màn hình gốc trong quá trình thực hành**, được sắp xếp theo nội dung tương ứng trong bài lab.

## 16.1. Kiểm tra Linux Basic và môi trường Ubuntu Server

Các lệnh được thực hành gồm:

```bash
whoami
pwd
ls
uname -a
hostname
cat /etc/os-release
echo $SHELL
```

![Linux Basic - kiểm tra môi trường](images/01-linux-basic-first-check.png)

Ảnh trên ghi nhận quá trình kiểm tra user, thư mục hiện tại, Kernel, hostname, phiên bản Ubuntu và Shell.

---

## 16.2. Kiểm tra lại môi trường Ubuntu Server 24.04

Ảnh này ghi nhận môi trường thực hành với:

```text
User: tungdd
Hostname: ubuntuserver2404
Ubuntu: 24.04.4 LTS
Shell: /bin/bash
```

![Ubuntu Server 24.04 environment](images/02-ubuntu-server-environment.png)

---

## 16.3. Thực hành Linux Filesystem

Các lệnh chính:

```bash
ls /
pwd
df -h
```

![Linux Filesystem](images/03-filesystem-check.png)

Ảnh cho thấy cấu trúc Root Directory `/`, Home Directory `/home/tungdd` và thông tin filesystem được mount trên hệ thống.

---

## 16.4. Phân tích Filesystem, Home, `/etc` và `/var/log`

Các lệnh được sử dụng:

```bash
ls -la /
ls -la /home/tungdd
ls -la /etc | head
ls -la /var/log | head
du -sh /home/tungdd
```

![Linux Filesystem detailed lab](images/04-filesystem-detailed-check.png)

Ảnh minh chứng cho việc quan sát quyền truy cập, owner/group, các file ẩn trong Home Directory, cấu trúc `/etc`, log trong `/var/log` và dung lượng `/home/tungdd`.

---

## 16.5. Liên hệ ảnh minh chứng với kiến thức

```text
Linux Basic
    ↓
Ubuntu Server
    ↓
Terminal
    ↓
Shell / Bash
    ↓
Filesystem
    ↓
File & Directory
    ↓
Permission
    ↓
Process
    ↓
Package
    ↓
Service
    ↓
Network
    ↓
Logs
```

Trong bài lab hiện tại, các phần từ **Linux Basic → Filesystem** đã được kiểm chứng bằng output thực tế và ảnh chụp màn hình.

Các phần **File & Directory → Logs** sẽ tiếp tục được bổ sung minh chứng khi thực hành.

> **Lưu ý:** Ảnh được giữ nguyên từ quá trình thực hành, không thay đổi nội dung output. Điều này giúp phân biệt rõ giữa kiến thức lý thuyết và kết quả thực tế trên server.
