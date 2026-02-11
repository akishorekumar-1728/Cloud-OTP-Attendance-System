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

## OTP Workflow (How Attendance Works)

1. Teacher selects a class → clicks **Generate OTP**
2. System saves OTP in DB with timestamp
3. Student enters OTP → system checks:

   * OTP matches
   * OTP is not expired (example: 60 seconds)
4. If valid → attendance record inserted with timestamp


