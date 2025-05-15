# Learn Git

### 1. สร้างไฟล์อะไรสักอย่าง (เช่น README.md)
echo "# Learn Git" > README.md

### 2. init git (ไม่จำเป็นจริงๆ เพราะ clone มาแล้ว แต่นี่เพื่อความมั่นใจว่ามี branch)
git init -b main

### 3. add ไฟล์เข้า staging area
git add .

### 4. commit ไฟล์ลง local repo
git commit -m "initial commit"

### 5. เชื่อม remote origin (ถ้ายังไม่เชื่อม)
git remote add origin https://github.com/cryptoclaw/learn-git.git

### 6. push ขึ้นไปที่ branch main พร้อมตั้งค่า upstream
git push -u origin main

` _คำอธิบายเพิ่มเติม_
error src refspec main does not match any แปลว่า ยังไม่มี branch main หรือยังไม่มี commit แรกเลย
เมื่อ clone repo เปล่า (empty repo) จะไม่มี branch จนกว่าจะมี commit แรก`

_เปลี่ยน remote ให้ Git ใช้ชื่อ cryptoclaw ของคุณ:_
git remote set-url origin https://<YOUR_GITHUB_USERNAME>@github.com/cryptoclaw/learn-git.git

_ลอง push ใหม่:_
git push -u origin main

_อีกวิธี : ใช้ SSH แทน HTTPS (สะดวกระยะยาว)_
สร้าง SSH key:
ssh-keygen -t ed25519 -C "your-email@example.com"
กด Enter ไปเรื่อย ๆ

_คัดลอก SSH public key:_
cat ~/.ssh/id_ed25519.pub
แล้วนำไปวางใน GitHub → Settings → SSH and GPG keys

_เปลี่ยน remote URL ให้ใช้ SSH:_
git remote set-url origin git@github.com:cryptoclaw/learn-git.git

_จากนั้น push:_
git push -u origin main

`✅ วิธีเช็กว่าใช้บัญชี GitHub ตัวไหนอยู่`
git config --global user.name
git config --global user.email

`หากไม่ใช่ของคุณ → เปลี่ยนเป็นของคุณ:`
git config --global user.name "cryptoclaw"
git config --global user.email "your-email@example.com"

`กรณี บน GitHub (remote) มี commit ที่ คุณไม่มีอยู่ในเครื่อง (local)
เลยไม่สามารถ push ได้ เพราะจะทำให้ข้อมูลบน GitHub หายไป (Git ป้องกันไว้)`

`✅ วิธีแก้ (ปลอดภัย):
ให้คุณ ดึงของบน GitHub มารวมกับของเรา (pull ก่อน push):`
git pull --rebase origin main
`--rebase จะดึง commit จาก GitHub แล้วเอา commit ของคุณมาต่อท้าย ไม่ทำให้เกิด merge commit รกๆ
เสร็จแล้วให้ push อีกครั้ง:`
git push -u origin main

`⚠️ หรือถ้าคุณมั่นใจว่าอยาก ลบของบน GitHub ทิ้งทั้งหมด แล้วเอาของคุณแทน:`
## git push -u origin main --force
`อันนี้อันตราย เพราะจะลบ commit ที่อยู่บน GitHub ทิ้งเลย — ใช้เฉพาะกรณีที่คุณแน่ใจว่าไม่มีอะไรสำคัญบน remote`

`✅ แนะนำ:
ใช้ pull --rebase ดีกว่า เพราะคุณจะได้ไม่ลบของเดิมที่อาจมีคนอื่น (หรือคุณเอง) เคย push ไว้`
