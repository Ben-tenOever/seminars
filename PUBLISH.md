# Publishing this site

Run these on your Mac, in Terminal. They will not work from a Claude session —
the cloud container has no access to your GitHub credentials.

## One time: create the repo and turn on Pages

```bash
# 1. Unzip somewhere sensible and go there
cd ~/Documents/seminars          # <- wherever you put the folder

# 2. Make sure gh is authenticated (skip if you already did this for the grants site)
gh auth status || gh auth login

# 3. Initialise and commit
git init -b main
git add .
git commit -m "Microbiology seminar series 2026-2027"

# 4. Create the repo on GitHub and push in one step
gh repo create seminars --public --source=. --remote=origin --push

# 5. Turn on GitHub Pages from main / (root)
gh api -X POST repos/ben-tenoever/seminars/pages \
  -f 'source[branch]=main' -f 'source[path]=/'
```

Wait two to five minutes, then check it is live:

```bash
curl -sI https://ben-tenoever.github.io/seminars/ | head -1
```

`HTTP/2 200` means it is up. A 404 usually just means Pages has not finished
building — wait and run it again.

## Every time after that

```bash
cd ~/Documents/seminars
git add -A
git commit -m "Update schedule"
git push
```

That is the whole update loop. Edit `index.html`, commit, push.

---

# Regenerating the QR code

`assets/qr_seminars.png` is already made and already on the slide, so you only
need this if the URL ever changes.

```bash
python3 -m pip install --user qrcode pillow

python3 - <<'EOF'
import qrcode
qr = qrcode.QRCode(error_correction=qrcode.constants.ERROR_CORRECT_Q,
                   box_size=20, border=2)
qr.add_data("https://ben-tenoever.github.io/seminars")
qr.make(fit=True)
qr.make_image(fill_color="#580F8B", back_color="white").save("qr_seminars.png")
print("wrote qr_seminars.png")
EOF
```

`ERROR_CORRECT_Q` is the 25% redundancy level — it survives a projector, a
phone camera at the back of the room, and someone's head in the way.

Check it before you trust it:

```bash
open qr_seminars.png     # then scan it with your phone
```
