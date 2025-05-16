# Learn Git

### 1. สร้างไฟล์อะไรสักอย่าง (เช่น README.md) \
echo "# Learn Git" > README.md \

### 2. init git (ไม่จำเป็นจริงๆ เพราะ clone มาแล้ว แต่นี่เพื่อความมั่นใจว่ามี branch) \
git init -b main \

### 3. add ไฟล์เข้า staging area \
```bash 
git add .
```

### 4. commit ไฟล์ลง local repo
```bash 
git commit -m "initial commit"
```
### 5. เชื่อม remote origin (ถ้ายังไม่เชื่อม)
```bash 
git remote add origin https://github.com/cryptoclaw/learn-git.git
```
### 6. push ขึ้นไปที่ branch main พร้อมตั้งค่า upstream
```bash 
git push -u origin main
```

### คำอธิบายเพิ่มเติม
`error src refspec main does not match any` แปลว่า ยังไม่มี `branch main` หรือยังไม่มี `commit` แรกเลย
เมื่อ `clone repo` เปล่า (empty repo) จะไม่มี `branch` จนกว่าจะมี `commit` แรก

เปลี่ยน remote ให้ Git ใช้ชื่อ cryptoclaw ของคุณ:
```bash 
git remote set-url origin https://<YOUR_GITHUB_USERNAME>@github.com/cryptoclaw/learn-git.git
```
_ลอง push ใหม่:_
```bash 
git push -u origin main
```

อีกวิธี : ใช้ SSH แทน HTTPS (สะดวกระยะยาว)
สร้าง SSH key:
```bash
ssh-keygen -t ed25519 -C "your-email@example.com"
```
กด Enter ไปเรื่อย ๆ

คัดลอก SSH public key:
```bash
cat ~/.ssh/id_ed25519.pub
```
แล้วนำไปวางใน GitHub → Settings → SSH and GPG keys

เปลี่ยน remote URL ให้ใช้ SSH:
```bash
git remote set-url origin git@github.com:cryptoclaw/learn-git.git
```

จากนั้น push:
```bash
git push -u origin main
```

✅ วิธีเช็กว่าใช้บัญชี GitHub ตัวไหนอยู่
```bash
git config --global user.name
```
```bash
git config --global user.email
```
หากไม่ใช่ของคุณ → เปลี่ยนเป็นของคุณ:
```bash
git config --global user.name "cryptoclaw"
```
```bash
git config --global user.email "your-email@example.com"
```

กรณี บน GitHub (remote) มี commit ที่ คุณไม่มีอยู่ในเครื่อง (local) \
เลยไม่สามารถ push ได้ เพราะจะทำให้ข้อมูลบน GitHub หายไป (Git ป้องกันไว้)

✅ วิธีแก้ (ปลอดภัย):
ให้คุณ ดึงของบน GitHub มารวมกับของเรา (pull ก่อน push):
```bash
git pull --rebase origin main
```
--rebase จะดึง commit จาก GitHub แล้วเอา commit ของคุณมาต่อท้าย ไม่ทำให้เกิด merge commit รกๆ
เสร็จแล้วให้ push อีกครั้ง:
```bash
git push -u origin main
```

จริงๆสามารถใช้ ```bash git push -f origin main ``` ได้เลย

⚠️ หรือถ้าคุณมั่นใจว่าอยาก ลบของบน GitHub ทิ้งทั้งหมด แล้วเอาของคุณแทน:
```bash git push -u origin main --force ```
อันนี้อันตราย เพราะจะลบ commit ที่อยู่บน GitHub ทิ้งเลย — ใช้เฉพาะกรณีที่คุณแน่ใจว่าไม่มีอะไรสำคัญบน remote

✅ แนะนำ:
ใช้ pull --rebase ดีกว่า เพราะคุณจะได้ไม่ลบของเดิมที่อาจมีคนอื่น (หรือคุณเอง) เคย push ไว้

clone git link on CMD or Terminal :
1. cd ..in to folder
2. git clone ..link...
   ขั้นตอนการเปิดโปรเจค on CMD or Terminal
3. cd ..name project
4. code . 

repository ในเครื่องของคุณเชื่อมกับ remote อะไรอยู่  (เช่น origin ไปที่ GitHub หรือที่อื่น) ให้ใช้คำสั่งนี้:
```bash git remote -v ```

ถ้าอยากดูรายละเอียดเพิ่มเติมของ remote \
```bash git remote show origin ```
จะบอกรายละเอียดเช่นว่า push/pull ไปที่ไหน, branch ไหน track อะไรอยู่ เป็นต้นครับ\
