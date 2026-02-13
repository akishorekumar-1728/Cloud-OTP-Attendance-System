## Project Statement

**Cloud Attendance System** is a role-based web application that automates classroom attendance using **OTP verification**.
Teachers generate a time-limited OTP for a class, students submit the OTP to mark attendance, and admins manage classes, schedules, and teacher-class mappings. The system is deployable on **Azure VM** and can run inside **Docker**.

---

## Key Features

### ✅ Common

* Role based login: **Admin / Teacher / Student**
* Session based authentication
* Responsive UI with sidebar navigation (base.html)
* SQLite database for all records

### ✅ Admin Features

* View latest attendance logs (student + class + readable time)
* **Manage Classes** (create new class: name, dept, class code)
* **Manage Schedule** for each class (day + start/end time)
* **Assign Teachers** to classes (teacher ↔ class mapping)

### ✅ Teacher Features

* Teacher dashboard showing assigned classes
* Generate OTP for selected class
* Teacher profile (name, dept)
* View class list + enrolled students

### ✅ Student Features

* Student dashboard to submit OTP
* Student profile (name + class info)
* Student schedule view (weekly timetable)
* Attendance history view (last 200 records)

---

## Tech Stack

### Backend

* **Python**
* **Flask** (routing, templates, sessions)

### Frontend

* **HTML + Jinja2 templates**
* **CSS** (custom UI)

### Database

* **SQLite** (`database.db`)
* Tables: users, classes, class_schedule, student_profile, teacher_profile, teacher_class, attendance, otp

### Deployment

* Local run: `python app.py`
* Cloud: **Azure VM**
* GitHub Actions CI/CD
* Containerization: **Docker**

---

## APIs / Libraries Used

### Flask APIs

* `Flask()` – app init
* `@app.route()` – route mapping
* `render_template()` – render HTML pages
* `request.form` – form inputs
* `session[]` – login session control
* `redirect()` – navigation
* `url_for()` – static file links

### Python Built-ins / Modules

* `sqlite3` – database operations
* `random` – OTP generation
* `time` – OTP expiry & timestamps
* `datetime` – readable timestamps
* `os` – DB path handling
* `functools.wraps` – decorators

---

## Project Setup (Local)

### 1) Clone

```bash
git clone https://github.com/akishorekumar-1728/cloud-attendance.git
cd cloud-attendance
```

### 2) Install requirements

```bash
pip install -r requirements.txt
```

### 3) Run

```bash
python app.py
```

### 4) Open

* `http://127.0.0.1:5000`

---

## Project Setup (Azure VM)

### 1) SSH into VM

```bash
ssh -i attendance-vm_key.pem azureuser@<VM_PUBLIC_IP>
```

### 2) Pull code + run

```bash
cd cloud-attendance
git pull origin main
pip install -r requirements.txt
python app.py
```

### 3) Open in browser

* `http://<VM_PUBLIC_IP>:5000`

---

## Project Setup (Docker)

### 1) Build

```bash
docker build -t cloud-attendance-app .
```

### 2) Run container

```bash
docker run -d -p 80:5000 --name cloud-attendance cloud-attendance-app
```

### 3) Open

* `http://<VM_PUBLIC_IP>/`

---
###Run with Docker

```bash
docker build -t cloud-attendance-app .
docker run -d -p 5000:5000 cloud-attendance-app
```

## OTP Workflow (How Attendance Works)

1. Teacher selects a class → clicks **Generate OTP**
2. System saves OTP in DB with timestamp
3. Student enters OTP → system checks:

   * OTP matches
   * OTP is not expired (example: 60 seconds)
4. If valid → attendance record inserted with timestamp

📸 Screenshots
<img width="1917" height="1021" alt="Screenshot 2026-02-13 163211" src="https://github.com/user-attachments/assets/1f4d61a7-42e9-4453-9c91-eabe2c5bdd17" />
<img width="1919" height="1029" alt="Screenshot 2026-02-13 163344" src="https://github.com/user-attachments/assets/e1f54714-f151-45b5-8c09-4988c7695c82" />
<img width="1899" height="902" alt="Screenshot 2026-02-13 163439" src="https://github.com/user-attachments/assets/48b0c9a1-30c7-408d-91ea-f5cd403b0d9f" />
<img width="844" height="636" alt="Screenshot 2026-02-13 163522" src="https://github.com/user-attachments/assets/6e95c331-aba4-4a69-8f66-786b77ec591e" />
<img width="789" height="635" alt="Screenshot 2026-02-13 163533" src="https://github.com/user-attachments/assets/8a3fcd6f-9b9e-4a79-bf79-fe5435a932bc" />
<img width="1327" height="595" alt="Screenshot 2026-02-13 163549" src="https://github.com/user-attachments/assets/42f9b618-2f1c-4e9c-a29c-727af0ffabf7" />
<img width="1918" height="863" alt="Screenshot 2026-02-13 163607" src="https://github.com/user-attachments/assets/6ab47c6c-01e3-43fd-9303-389a73bdadf4" />
<img width="1919" height="896" alt="Screenshot 2026-02-13 163656" src="https://github.com/user-attachments/assets/83fe1efc-5e7e-43b3-a368-2b0f67583667" />
<img width="1917" height="883" alt="Screenshot 2026-02-13 163741" src="https://github.com/user-attachments/assets/0636f518-f698-4f9b-9ea3-3f6268647848" />
<img width="1908" height="671" alt="Screenshot 2026-02-13 163841" src="https://github.com/user-attachments/assets/95eb78aa-ed86-490c-97ad-4b51c5531f12" />
<img width="1919" height="708" alt="Screenshot 2026-02-13 163855" src="https://github.com/user-attachments/assets/5549e35b-b3ce-4c8e-a8f6-19c8042e8da4" />
<img width="1919" height="585" alt="Screenshot 2026-02-13 163909" src="https://github.com/user-attachments/assets/568eeb01-4de6-4c83-8c1d-050098746931" />
<img width="1898" height="613" alt="Screenshot 2026-02-13 163923" src="https://github.com/user-attachments/assets/cccc647f-9a68-40ae-83bd-e369e3156318" />
<img width="1902" height="737" alt="Screenshot 2026-02-13 164143" src="https://github.com/user-attachments/assets/de82f30c-b30e-4daf-8955-fe98410ebfb2" />
<img width="1917" height="812" alt="Screenshot 2026-02-13 164154" src="https://github.com/user-attachments/assets/10a04fbe-efac-41af-a9ca-cc378f7e2556" />
<img width="1919" height="534" alt="Screenshot 2026-02-13 164203" src="https://github.com/user-attachments/assets/ad774bfe-f70a-4911-8deb-0a5e49cdd570" />
<img width="1919" height="511" alt="Screenshot 2026-02-13 164213" src="https://github.com/user-attachments/assets/0ac75d9a-4894-4c88-9540-1d6fc7896857" />




👨‍💻 Author

 A Kishore Kumar
🎓 B.Tech IT Student



LinkedIn:
https://www.linkedin.com/in/a-kishore-kumar-ba310a291


