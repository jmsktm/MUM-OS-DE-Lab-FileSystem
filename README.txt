
#######################################
#                                     #
#  LAB 3 (FILE SYSTEM)                #
#                                     #
#  Submitted by: James Singh          #
#  Student ID: 983976                 #
#  Subject: Operating Systems         #
#  Date: 06/28/2015                   #
#                                     #
#######################################




=======================================
==  LAB 3 QUESTION 1                 ==
=======================================

Use mkfs to create a file system with a block size of 64 bytes and having a total of 8 blocks. How many index nodes will fit in a block? How many directory entries will fit in a block? Use dump to examine the file system backing file, and note the value in byte 64. What does this value represent? Use mkdir to create a directory (e.g., /usr), and then use dump to examine byte 64 again. What do you notice? Repeat the process of creating a directory (e.g., /bin, /lib, /var, /etc, /home, /mnt, etc.) and examining with dump. How many directories can you create before you fill up the file system? Explain why.

Created a filesystem filesys.dat so that it contains eight 64 byte blocks for a total of 512 bytes.

java mkfs filesys.dat 64 8

The output from the command was:

block_size: 64
blocks: 8
super_blocks: 1
free_list_blocks: 1
inode_blocks: 3
data_blocks: 3
block_total: 8

Each inode requires 64 bytes. Since every block is 64 bytes in size, there will only be 1 inode per block.
Each directory entry requires 16 bytes. So, 64/16 =  4 directory entries will fit in a 64 byte block.

Printing the dump for filesys.dat using command 'java dump filesys.dat', we get:

1 40 64 @
5 8 8
9 1 1
13 2 2
17 5 5
64 1 1
128 40 64 @
131 3 3
139 20 32  
143 ff 255
144 ff 255
145 ff 255
146 ff 255
147 ff 255
148 ff 255
149 ff 255
150 ff 255
151 ff 255
152 ff 255
153 ff 255
154 ff 255
155 ff 255
156 ff 255
157 ff 255
158 ff 255
159 ff 255
160 ff 255
161 ff 255
162 ff 255
163 ff 255
164 ff 255
165 ff 255
166 ff 255
167 ff 255
168 ff 255
169 ff 255
322 2e 46 .
338 2e 46 .
339 2e 46 .

In block 64, we have value '1'. This means 1 block was allocated.

Created folder /usr using:
java mkdir /usr

Another dump:
java dump filesys.dat

1 40 64 @
5 8 8
9 1 1
13 2 2
17 5 5
64 3 3
128 40 64 @
131 3 3
139 30 48 0
143 ff 255
144 ff 255
145 ff 255
146 ff 255
147 ff 255
148 ff 255
149 ff 255
150 ff 255
151 ff 255
152 ff 255
153 ff 255
154 ff 255
155 ff 255
156 ff 255
157 ff 255
158 ff 255
159 ff 255
160 ff 255
161 ff 255
162 ff 255
163 ff 255
164 ff 255
165 ff 255
166 ff 255
167 ff 255
168 ff 255
169 ff 255
192 40 64 @
195 1 1
203 20 32  
206 1 1
207 ff 255
208 ff 255
209 ff 255
210 ff 255
211 ff 255
212 ff 255
213 ff 255
214 ff 255
215 ff 255
216 ff 255
217 ff 255
218 ff 255
219 ff 255
220 ff 255
221 ff 255
222 ff 255
223 ff 255
224 ff 255
225 ff 255
226 ff 255
227 ff 255
228 ff 255
229 ff 255
230 ff 255
231 ff 255
232 ff 255
233 ff 255
322 2e 46 .
338 2e 46 .
339 2e 46 .
353 1 1
354 75 117 u
355 73 115 s
356 72 114 r
385 1 1
386 2e 46 .
402 2e 46 .
403 2e 46 .


Again:
java mkdir /bin

java dump filesys.dat
1 40 64 @
5 8 8
9 1 1
13 2 2
17 5 5
64 7 7
128 40 64 @
131 3 3
139 40 64 @
143 ff 255
144 ff 255
145 ff 255
146 ff 255
147 ff 255
148 ff 255
149 ff 255
150 ff 255
151 ff 255
152 ff 255
153 ff 255
154 ff 255
155 ff 255
156 ff 255
157 ff 255
158 ff 255
159 ff 255
160 ff 255
161 ff 255
162 ff 255
163 ff 255
164 ff 255
165 ff 255
166 ff 255
167 ff 255
168 ff 255
169 ff 255
192 40 64 @
195 1 1
203 20 32  
206 1 1
207 ff 255
208 ff 255
209 ff 255
210 ff 255
211 ff 255
212 ff 255
213 ff 255
214 ff 255
215 ff 255
216 ff 255
217 ff 255
218 ff 255
219 ff 255
220 ff 255
221 ff 255
222 ff 255
223 ff 255
224 ff 255
225 ff 255
226 ff 255
227 ff 255
228 ff 255
229 ff 255
230 ff 255
231 ff 255
232 ff 255
233 ff 255
256 40 64 @
259 1 1
267 20 32  
270 2 2
271 ff 255
272 ff 255
273 ff 255
274 ff 255
275 ff 255
276 ff 255
277 ff 255
278 ff 255
279 ff 255
280 ff 255
281 ff 255
282 ff 255
283 ff 255
284 ff 255
285 ff 255
286 ff 255
287 ff 255
288 ff 255
289 ff 255
290 ff 255
291 ff 255
292 ff 255
293 ff 255
294 ff 255
295 ff 255
296 ff 255
297 ff 255
322 2e 46 .
338 2e 46 .
339 2e 46 .
353 2 2
354 62 98 b
355 69 105 i
356 6e 110 n
369 1 1
370 75 117 u
371 73 115 s
372 72 114 r
385 1 1
386 2e 46 .
402 2e 46 .
403 2e 46 .
449 2 2
450 2e 46 .
466 2e 46 .
467 2e 46 .


java mkdir /lib
mkdir: No space left on device
mkdir: "/lib"

The 3 available inodes were used during creation of directories /, /usr and /bin. So no more folders could be created.

/ : 1st inode (128-191)
/usr : 2nd inode (192 to 254)
/bin : 3rd inode (255 to 319)




=======================================
==  LAB 3 QUESTION 2                 ==
=======================================

Code submitted