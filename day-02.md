# Day 2: Subnetting with the Block Method

**Level 1, Month 1, Networking foundations**

## What I learned

My own method (table of blocks) is the standard one, so I worked with it, using the French terms I learned in class:

1. Bits d'hote (host bits) = 32 - prefix
2. Taille du bloc (block size) = 2^(host bits)
3. Draw the table of blocks: 0, size, 2 x size, ...
4. Find the block that contains the address, then fill in:
   - Adresse reseau = the start of the block
   - Premiere adresse = reseau + 1
   - Broadcast = start of the next block - 1
   - Derniere adresse = broadcast - 1

| Prefix | Bits d'hote | Taille du bloc | Valid hosts |
|---|---|---|---|
| /24 | 8 | 256 | 254 |
| /26 | 6 | 64 | 62 |
| /27 | 5 | 32 | 30 |
| /28 | 4 | 16 | 14 |
| /29 | 3 | 8 | 6 |

**Self-check:** Derniere must always come right before Broadcast.

## Problems solved

| Address | Reseau | Premiere | Broadcast | Derniere |
|---|---|---|---|---|
| 192.168.10.77/24 | 192.168.10.0 | 192.168.10.1 | 192.168.10.255 | 192.168.10.254 |
| 192.168.1.130/26 | 192.168.1.128 | 192.168.1.129 | 192.168.1.191 | 192.168.1.190 |
| 192.168.1.200/26 | 192.168.1.192 | 192.168.1.193 | 192.168.1.255 | 192.168.1.254 |
| 192.168.1.45/27 | 192.168.1.32 | 192.168.1.33 | 192.168.1.63 | 192.168.1.62 |
| 192.168.1.100/27 | 192.168.1.96 | 192.168.1.97 | 192.168.1.127 | 192.168.1.126 |
| 192.168.5.70/28 | 192.168.5.64 | 192.168.5.65 | 192.168.5.79 | 192.168.5.78 |
| 192.168.8.140/28 | 192.168.8.128 | 192.168.8.129 | 192.168.8.143 | 192.168.8.142 |
| 172.16.3.77/29 | 172.16.3.72 | 172.16.3.73 | 172.16.3.79 | 172.16.3.78 |

## Error log

| Mistake | Correct answer | Why |
|---|---|---|
| Valid hosts in /24: 253 | 254 | Started from 255. There are 256 addresses (0 to 255), minus 2. |
| 192.168.1.130/26: broadcast .255, last .254 | .191 and .190 | Used the /24 values. The block size is 64, so the block 128 ends at 191. |
| 192.168.1.200/26: broadcast .223, last .222 | .255 and .254 | Added 32 instead of 64. 192 + 64 - 1 = 255. |
| Host bits in /27: wrote 32 | 5 | 32 is the block size, not the number of host bits. |
| 192.168.197 | 192.168.1.97 | Missing dot. An address always has 4 numbers. |
| 192.168.5.70/28: started the block at 70 | Block starts at 64 | The block does not start at the given address. It starts at the nearest multiple of the block size below it. |
| 172.16.8.78 | 172.16.3.78 | Typing slip in the third number. Re-read the address before sending. |

## Main lessons

- Almost every mistake was about the **block size**. Rule: end of block = start + size - 1.
- The block never starts at the given address. It starts at the largest multiple of the block size that does not exceed it.
- Writing the label next to each line (Reseau, Premiere, Broadcast, Derniere) avoids order mix-ups.
- Re-read each address for typos before sending.

## Anki

Reviewed the 6 cards from Day 1 (forgot 2, relearned them in the same session).

## Next session

Subnets where the blocks fall in the third octet (/20, /22), then a first look at a pcap file.
