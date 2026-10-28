# Subnetting Practice Workbook

## Overview
A collection of **15 solved subnetting problems** covering CIDR notation and VLSM (Variable Length Subnet Masking), completed as part of the **Beginner — Foundations** track (Core Networking) at Kiriri Women's University of Science and Technology, Dept. of Computer Science & IT.

Each problem shows the given network, the required subnetting task, and a fully worked solution.

---

## Part A — CIDR Subnetting Problems

### Problem 1
**Given:** `192.168.10.0/24` — Divide into 4 equal subnets.

| Subnet | Network Address | Subnet Mask | First Usable | Last Usable | Broadcast |
|--------|------------------|-------------|----------------|----------------|-----------|
| 1 | 192.168.10.0/26 | 255.255.255.192 | 192.168.10.1 | 192.168.10.62 | 192.168.10.63 |
| 2 | 192.168.10.64/26 | 255.255.255.192 | 192.168.10.65 | 192.168.10.126 | 192.168.10.127 |
| 3 | 192.168.10.128/26 | 255.255.255.192 | 192.168.10.129 | 192.168.10.190 | 192.168.10.191 |
| 4 | 192.168.10.192/26 | 255.255.255.192 | 192.168.10.193 | 192.168.10.254 | 192.168.10.255 |

**Explanation:** /24 → /26 borrows 2 bits (2² = 4 subnets), giving 64 addresses per subnet (62 usable).

---

### Problem 2
**Given:** `10.0.0.0/8` — Subnet to support 500 hosts per subnet.

- Hosts needed: 500 → need 2⁹ = 512 (9 host bits) → borrow bits until host bits = 9 → `/23`
- **Subnet mask:** 255.255.254.0
- **Subnet size:** 512 addresses (510 usable)
- Example subnet: `10.0.0.0/23` → usable range `10.0.0.1 – 10.0.1.254`, broadcast `10.0.1.255`

---

### Problem 3
**Given:** `172.16.0.0/16` — Create subnets for 6 departments.

- Need 6 subnets → 2³ = 8 (round up to nearest power of 2) → borrow 3 bits → `/19`
- **Subnet mask:** 255.255.224.0
- First 3 subnets:
  | Subnet | Network | Range |
  |--------|---------|-------|
  | 1 | 172.16.0.0/19 | 172.16.0.1 – 172.16.31.254 |
  | 2 | 172.16.32.0/19 | 172.16.32.1 – 172.16.63.254 |
  | 3 | 172.16.64.0/19 | 172.16.64.1 – 172.16.95.254 |

---

### Problem 4
**Given:** `192.168.1.0/24` — Subnet into 8 equal parts.

- 2³ = 8 subnets → borrow 3 bits → `/27`, mask `255.255.255.224`, block size 32
- Subnets: .0, .32, .64, .96, .128, .160, .192, .224 (each /27, 30 usable hosts)

---

### Problem 5
**Given:** IP `172.20.14.68/20` — Find network address, broadcast, and usable range.

- /20 → mask 255.255.240.0, block size in 3rd octet = 16
- Network multiples of 16: ...0, 16, **32**... → 14 falls between 0–15 → Network = `172.20.0.0`
- **Network:** 172.20.0.0
- **Broadcast:** 172.20.15.255
- **Usable range:** 172.20.0.1 – 172.20.15.254

---

### Problem 6
**Given:** `203.0.113.0/28` — How many usable hosts?

- /28 → 2^(32-28) = 16 addresses → 16 - 2 = **14 usable hosts**
- Network: 203.0.113.0, Broadcast: 203.0.113.15, Range: .1 – .14

---

### Problem 7
**Given:** IP `10.15.200.5`, mask `255.255.255.128`. Which subnet does it belong to?

- /25, block size 128 → multiples: 0, 128 → 5 falls in the 0–127 block
- **Subnet:** 10.15.200.0/25
- **Broadcast:** 10.15.200.127
- **Range:** 10.15.200.1 – 10.15.200.126

---

### Problem 8
**Given:** `192.168.100.0/24` — Need 2 subnets, one for 100 hosts, one for 50 hosts (VLSM preview).

- 100 hosts → need 7 host bits (2⁷=128) → `/25` → 192.168.100.0/25 (126 usable)
- 50 hosts → need 6 host bits (2⁶=64) → `/26` → 192.168.100.128/26 (62 usable)

---

## Part B — VLSM (Variable Length Subnet Masking) Problems

### Problem 9
**Given:** `192.168.20.0/24`. Allocate for: Sales (60 hosts), IT (28 hosts), Guest Wi-Fi (12 hosts).

| Department | Hosts Needed | Prefix | Subnet | Range | Broadcast |
|------------|---------------|--------|--------|-------|-----------|
| Sales | 60 | /26 (62 usable) | 192.168.20.0/26 | .1–.62 | .63 |
| IT | 28 | /27 (30 usable) | 192.168.20.64/27 | .65–.94 | .95 |
| Guest Wi-Fi | 12 | /28 (14 usable) | 192.168.20.96/28 | .97–.110 | .111 |

**Method:** Allocate largest requirement first to avoid fragmentation, then work down.

---

### Problem 10
**Given:** `10.10.0.0/22`. Allocate for: HQ (200 hosts), Branch A (100 hosts), Branch B (50 hosts), WAN link (2 hosts).

| Segment | Hosts | Prefix | Subnet | Broadcast |
|---------|-------|--------|--------|-----------|
| HQ | 200 | /24 (254 usable) | 10.10.0.0/24 | 10.10.0.255 |
| Branch A | 100 | /25 (126 usable) | 10.10.1.0/25 | 10.10.1.127 |
| Branch B | 50 | /26 (62 usable) | 10.10.1.128/26 | 10.10.1.191 |
| WAN link | 2 | /30 (2 usable) | 10.10.1.192/30 | 10.10.1.195 |

---

### Problem 11
**Given:** `172.16.10.0/24`. Allocate for: Engineering (50), Marketing (25), Finance (10), Point-to-point router link (2).

| Segment | Hosts | Prefix | Subnet | Broadcast |
|---------|-------|--------|--------|-----------|
| Engineering | 50 | /26 | 172.16.10.0/26 | .63 |
| Marketing | 25 | /27 | 172.16.10.64/27 | .95 |
| Finance | 10 | /28 | 172.16.10.96/28 | .111 |
| Router link | 2 | /30 | 172.16.10.112/30 | .115 |

---

### Problem 12
**Given:** `192.168.5.0/25`. Split into 3 unequal subnets: Lab1 (28 hosts), Lab2 (14 hosts), Server room (6 hosts).

| Segment | Hosts | Prefix | Subnet | Broadcast |
|---------|-------|--------|--------|-----------|
| Lab1 | 28 | /27 | 192.168.5.0/27 | .31 |
| Lab2 | 14 | /28 | 192.168.5.32/28 | .47 |
| Server room | 6 | /29 | 192.168.5.48/29 | .55 |

---

### Problem 13
**Given:** `10.0.0.0/16`. Allocate for 3 buildings: Building A (500 hosts), Building B (250 hosts), Building C (100 hosts).

| Segment | Hosts | Prefix | Subnet | Broadcast |
|---------|-------|--------|--------|-----------|
| Building A | 500 | /23 | 10.0.0.0/23 | 10.0.1.255 |
| Building B | 250 | /24 | 10.0.2.0/24 | 10.0.2.255 |
| Building C | 100 | /25 | 10.0.3.0/25 | 10.0.3.127 |

---

### Problem 14
**Given:** Calculate the number of subnets and hosts for `/29` and `/30` on a `192.168.0.0/24` block.

- `/29`: 2^(29-24)=32 subnets, each with 2^(32-29)-2 = **6 usable hosts**
- `/30`: 2^(30-24)=64 subnets, each with 2^(32-30)-2 = **2 usable hosts** (typical for router-to-router links)

---

### Problem 15
**Given:** A company has `172.30.4.0/22` and needs 4 subnets of equal size for 4 floors, each requiring at least 100 hosts.

- /22 has 1024 addresses total. Need 4 equal subnets → borrow 2 bits → `/24` each (254 usable — meets the ≥100 requirement)

| Floor | Subnet | Range | Broadcast |
|-------|--------|-------|-----------|
| 1 | 172.30.4.0/24 | .1–.254 | 172.30.4.255 |
| 2 | 172.30.5.0/24 | .1–.254 | 172.30.5.255 |
| 3 | 172.30.6.0/24 | .1–.254 | 172.30.6.255 |
| 4 | 172.30.7.0/24 | .1–.254 | 172.30.7.255 |

---

## Key Formulas Reference

| Concept | Formula |
|---------|---------|
| Number of subnets | 2ⁿ (n = bits borrowed) |
| Hosts per subnet | 2ʰ - 2 (h = remaining host bits) |
| Block size | 256 - (last non-255/non-0 octet of mask) |

## Author
[Janet wanjiru] — Kiriri Women's University of Science and Technology, Dept. of Computer Science & IT
