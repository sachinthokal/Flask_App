# Flask Python Website Deployment (End‑to‑End – One‑Line Steps)

> **Example:** Simple Flask app on Ubuntu server using Nginx + Gunicorn

---

## 1️⃣ Server Prep
- Create Ubuntu VM → Open ports **22, 80, 443** → SSH into server

## 2️⃣ Install Basics
- `sudo apt update && sudo apt install python3-pip python3-venv nginx git -y`

## 3️⃣ App Folder
- `mkdir /var/www/flaskapp && cd /var/www/flaskapp`

## 4️⃣ Virtual Environment
- `python3 -m venv venv && source venv/bin/activate`

## 5️⃣ Flask Install
- `pip install flask gunicorn`

## 6️⃣ Create Flask App
- Create file `app.py`:
```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def home():
    return "Hello from Flask Website 🚀"
```

## 7️⃣ Test Flask App
- `python app.py` or `flask run --host=0.0.0.0 --port=8000` → check in browser

## 8️⃣ Gunicorn Test
- `gunicorn app:app --bind 127.0.0.1:8000`

## 9️⃣ Nginx Config
- Create file `/etc/nginx/sites-available/flaskapp`
```nginx
server {
    listen 80;
    server_name _;

    location / {
        proxy_pass http://127.0.0.1:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

## 🔟 Enable Nginx Config
- `sudo ln -s /etc/nginx/sites-available/flaskapp /etc/nginx/sites-enabled`

## 1️⃣1️⃣ Restart Nginx
- `sudo nginx -t && sudo systemctl restart nginx`

## 1️⃣2️⃣ Run as Service (Optional but Recommended)
- Create systemd service for Gunicorn and enable it

## 1️⃣3️⃣ Final Check
- Open browser → `http://SERVER-IP` → Flask page live 🎉

---

## 🧠 One‑Line Flow (Interview Ready)
> **Browser → Nginx → Gunicorn → Flask App**

---

## 📌 Notes
- Public IP = required
- No Docker / AKS here (pure VM deployment)
- HTTPS can be added later using Certbot

---

✅ **This is the simplest real‑world Flask deployment flow.**

