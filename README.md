# 🖥️ My First Cybersecurity Lab Setup

**Week 1 Project | VirtualBox + Kali Linux**

---

## 📌 About This Project

For my first week project I built a small cybersecurity lab on my own laptop. It uses VirtualBox and a Kali Linux virtual machine, connected through a private NAT Network. The idea is to have a safe place to practice security tools without risking my real computer or my home network.

Only use a lab like this on systems you own or have permission to test.

![Kali Linux desktop](kali-desktop.png)

---

## 🎯 What I Did

- Installed VirtualBox
- Installed Kali Linux as a virtual machine
- Created a custom NAT Network, so the lab has its own separate subnet
- Set up a shared folder between my Windows computer and Kali
- Configured the IP address on Kali
- Checked that the internet and DNS still worked
- Took a clean snapshot so I can restore it if something breaks

---

## ⚙️ Lab Details

| Item | Details |
| --- | --- |
| Host OS | Windows [10/11] |
| Hypervisor | VirtualBox [version] |
| Guest OS | Kali Linux [version] |
| Network type | NAT Network |
| Lab subnet | 10.0.0.0/24 |
| Kali IP | 10.0.0.2/24 |
| Gateway | 10.0.0.1 |
| DNS | 8.8.8.8 |

---

## 🪜 Setup Steps

### Step 1: Install VirtualBox
Downloaded VirtualBox from the official website and installed it on Windows.

### Step 2: Download and import Kali Linux
Downloaded the Kali VM image from the official Kali website and imported it into VirtualBox.

### Step 3: Create the NAT Network
In VirtualBox I created a new NAT Network with its own IP range. I chose a NAT Network (not plain NAT) so more VMs can join the same network later and talk to each other.

![NAT Network settings](nat-network.png)

### Step 4: Connect Kali to the NAT Network
In the Kali VM settings, I set Adapter 1 to "NAT Network" and picked the network I created.

### Step 5: Set up the shared folder
I added a shared folder in VirtualBox so I can move files between Windows and Kali. In Kali it shows up under `/media/sf_<foldername>`.

### Step 6: Configure the IP address
I changed Kali's IP address from the automatic one to `10.0.0.2/24` using the IPv4 settings.

![Kali IPv4 settings](kali-ipv4-settings.png)

Then I checked it with:

```
ip a
ip route
```

![ip a and ip route output](ip-a-route.png)

### Step 7: Take a snapshot
Once everything was working, I took a clean snapshot named `[your snapshot name]`.

---

## 🔎 How I Checked It Worked

| Check | Command | What I expected |
| --- | --- | --- |
| IP address | `ip a` | Shows 10.0.0.2/24 |
| Gateway | `ip route` | Shows the default route |
| Internet and DNS | `ping -c 3 google.com` | Name resolves, replies received |
| Short IP view | `ip -br a` | Shows the interface and its IP |
| Shared folder | `ls -la /media/sf_kali_downloads` | Folder opens, files are listed |

![Verification commands](verification.png)

I also opened Firefox to make sure normal browsing works.

![Firefox working](firefox-working.png)

---

## 🐞 Problems I Ran Into

### Problem 1: Kali wouldn't finish downloading
The download kept failing and nothing I tried fixed it. In the end, switching to a different network (my hotspot) let it finish. Sometimes the problem is the network, not your setup.

### Problem 2: Getting the right IP address
Kali kept getting `10.0.0.3` automatically, but I needed `10.0.0.2`. When I changed the settings, I lost my internet and had to troubleshoot it. I got it working again by resetting the connection and then setting the address manually. After that I verified it with `ip a`.

### Problem 3: Finding the shared folder
At first Kali couldn't find my shared folder. It turned out Linux mounts shared folders under `/media` with an `sf_` prefix, and I had picked a folder in the wrong location on my host. Fixing that solved it.

---

## 💡 What I Learned

- Take a snapshot **before** changing network settings, not after.
- Check your real gateway with `ip route` instead of guessing it.
- A successful ping doesn't always mean the connection is healthy.
- Read error messages slowly. They usually point to the problem.
- If a download won't finish, try another network before blaming your setup.
- Writing down problems and fixes is part of the work.

---

## 🔗 Tools Used

- VirtualBox: https://www.virtualbox.org/wiki/Downloads
- Kali Linux: https://www.kali.org/get-kali/

---

## 👤 Author

**Areeha Qamar**
Cybersecurity Intern, Network Walks Academy
LinkedIn: www.linkedin.com/in/areeha-qamar422

**Week:** 01
**Project:** Cybersecurity Lab Setup
