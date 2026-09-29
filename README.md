# JARKOM SIMULASI P2 VLAN

## Deskripsi
Proyek ini berisi simulasi jaringan VLAN dan Inter‑VLAN Routing menggunakan Cisco Packet Tracer. Tujuannya untuk memahami konsep pemisahan jaringan berdasarkan VLAN serta cara komunikasi antar‑VLAN melalui router.

## Tujuan Pembelajaran
- Memahami konsep dasar VLAN dan manfaatnya dalam manajemen jaringan.  
- Mengetahui cara konfigurasi VLAN pada switch.  
- Mempelajari konfigurasi sub‑interface router untuk inter‑VLAN routing.  
- Melatih keterampilan troubleshooting jaringan menggunakan perintah `ping`.  
- Menyusun dokumentasi praktikum dengan hasil pengujian yang jelas.

## Konfigurasi VLAN
| VLAN | Network | Gateway |
|------|----------|---------|
| VLAN 10 | 192.168.10.0/24 | 192.168.10.1 |
| VLAN 20 | 192.168.20.0/24 | 192.168.20.1 |

## Perangkat
- 1 Router Cisco 2911  
- 2 Switch  
- 5 PC  
- Cisco Packet Tracer  

## Diagram Topologi (sederhana)
[PC1]---+
| VLAN 10
[PC2]---+         +---[Router]---+
|               |
[PC3]---+         | VLAN 20       |
| VLAN 20 |               |
[PC4]---+         +---------------+
[PC5]---+

<img width="661" height="403" alt="image" src="https://github.com/user-attachments/assets/8a98b391-d3a2-4894-a5ba-41fe435fb371" />

## Konfigurasi Router (CLI)
Router> enable
Router# configure terminal
Router(config)# interface g0/0
Router(config-if)# no shutdown

! Sub-interface untuk VLAN 10
Router(config)# interface g0/0.10
Router(config-subif)# encapsulation dot1Q 10
Router(config-subif)# ip address 192.168.10.1 255.255.255.0

! Sub-interface untuk VLAN 20
Router(config)# interface g0/0.20
Router(config-subif)# encapsulation dot1Q 20
Router(config-subif)# ip address 192.168.20.1 255.255.255.0

## Konfigurasi Switch (CLI)
Switch> enable
Switch# configure terminal

! Membuat VLAN
Switch(config)# vlan 10
Switch(config-vlan)# name VLAN10
Switch(config)# vlan 20
Switch(config-vlan)# name VLAN20

! Assign port ke VLAN 10
Switch(config)# interface fastEthernet0/1
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 10

Switch(config)# interface fastEthernet0/2
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 10

! Assign port ke VLAN 20
Switch(config)# interface fastEthernet0/3
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 20

Switch(config)# interface fastEthernet0/4
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 20

! Port trunk ke router
Switch(config)# interface fastEthernet0/24
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk allowed vlan 10,20

## Langkah Konfigurasi
1. Buat VLAN 10 dan VLAN 20 pada masing‑masing switch.  
2. Atur port sesuai dengan VLAN yang ditentukan.  
3. Konfigurasikan sub‑interface pada router untuk setiap VLAN.  
4. Berikan IP gateway sesuai tabel konfigurasi di atas.  
5. Lakukan pengujian konektivitas antar‑PC menggunakan perintah `ping`.

## Pengujian
Pengujian dilakukan untuk memastikan komunikasi antar‑VLAN berjalan dengan baik.

**Hasil pengujian:**
- 192.168.20.100 → 192.168.20.1 : berhasil  
- 192.168.20.100 → 192.168.10.1 : berhasil  
- 192.168.20.100 → 192.168.10.150 : berhasil, 0% packet loss

## Troubleshooting
- Jika ping gagal, cek apakah IP address di PC sudah sesuai VLAN.  
- Pastikan port yang digunakan sudah di‑assign ke VLAN yang benar.  
- Periksa konfigurasi trunk pada port yang terhubung ke router.  
- Gunakan perintah `show vlan brief` di switch untuk melihat status VLAN.  
- Gunakan perintah `show ip interface brief` di router untuk memastikan sub‑interface aktif.

## File
`JARKOM SIMULASI P2 VLAN.pkt`

## Cara Menjalankan Simulasi
1. Buka file `.pkt` menggunakan Cisco Packet Tracer.  
2. Pastikan semua perangkat aktif dan terhubung sesuai topologi.  
3. Jalankan perintah `ping` antar‑PC untuk melihat hasil komunikasi.  
4. Simpan hasil pengujian sebagai dokumentasi praktikum.

---
README ini disusun untuk dokumentasi praktikum Jaringan Komputer – Simulasi VLAN dan Inter‑VLAN Routing.
Catatan: Konfigurasi dapat berbeda tergantung versi Packet Tracer yang digunakan.
## File
[Download JARKOM SIMULASI P2 VLAN.pkt](./JARKOM%20SIMULASI%20P2%20VLAN.pkt)



