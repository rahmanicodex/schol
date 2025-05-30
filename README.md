
<html lang="fa" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <title>سامانه مدیریت مکتب افغان</title>
  <link href="https://fonts.googleapis.com/css2?family=Vazirmatn&display=swap" rel="stylesheet" />
  <link
    rel="stylesheet"
    href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css"
  />
  <style>
    * {
      font-family: 'Vazirmatn', sans-serif;
    }
    body {
      background: url('https://images.unsplash.com/photo-1577896851231-70ef18881754?ixlib=rb-4.0.3&auto=format&fit=crop&w=1350&q=80')
        no-repeat center center fixed;
      background-size: cover;
      margin: 0;
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      direction: rtl;
    }
    .container,
    .admin-panel,
    .teacher-panel,
    .parent-panel {
      background-color: rgba(255, 255, 255, 0.95);
      border-radius: 15px;
      padding: 30px;
      width: 90%;
      max-width: 600px;
      box-shadow: 0 0 20px rgba(0, 0, 0, 0.3);
      text-align: center;
    }
    h1,
    h2,
    h3 {
      color: #1d3557;
      margin-bottom: 15px;
    }
    input,
    select,
    textarea {
      width: 100%;
      padding: 10px;
      margin-top: 10px;
      border-radius: 10px;
      border: 1px solid #ccc;
      box-sizing: border-box;
      font-size: 16px;
      font-family: 'Vazirmatn', sans-serif;
    }
    button {
      width: 100%;
      padding: 12px;
      background-color: #1d3557;
      color: white;
      border: none;
      border-radius: 10px;
      margin-top: 15px;
      font-size: 18px;
      cursor: pointer;
      transition: background-color 0.3s;
    }
    button:hover {
      background-color: #0d1c34;
    }
    .hidden {
      display: none;
    }
    .record {
      background-color: #f0f8ff;
      border-left: 6px solid #1d3557;
      border-radius: 10px;
      padding: 18px 22px;
      margin-top: 18px;
      text-align: right;
      font-size: 1.1rem;
      color: #2a2a2a;
      box-shadow: 0 3px 8px rgba(0, 0, 0, 0.1);
      line-height: 1.6;
      font-weight: 600;
    }
    .record b {
      color: #1d3557;
      display: inline-block;
      min-width: 120px;
    }
    .school-info {
      margin-top: 20px;
      text-align: right;
      font-size: 14px;
      line-height: 1.8;
      color: #333;
    }
    .school-info i {
      margin-left: 8px;
      color: #1d3557;
    }
    .user-list {
      text-align: right;
      margin-top: 20px;
    }
    .user-item {
      background: #f1f1f1;
      padding: 10px;
      border-radius: 8px;
      margin-top: 10px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: 10px;
    }
    .user-item input {
      margin: 0 5px;
      padding: 6px 10px;
      font-size: 15px;
      border-radius: 6px;
      border: 1px solid #ccc;
      flex: 1;
    }
    a {
      color: #1d3557;
      text-decoration: none;
    }
    a:hover {
      text-decoration: underline;
    }
  </style>
</head>
<body>
  <div class="container" id="login-panel">
    <h1>سامانه مدیریت مکتب خصوصی بامیکا</h1>
    <div class="school-info">
      <p><i class="fas fa-map-marker-alt"></i> آدرس: کابل، دشت برچی، ریگریشن</p>
      <p><i class="fas fa-phone"></i> شماره تماس: ۰۷۰۰۱۲۳۴۵۶</p>
      <p><i class="fab fa-whatsapp"></i> واتساپ: ۰۷۰۰۱۲۳۴۵۶</p>
      <p>
        <i class="fab fa-telegram"></i> کانال تلگرام:
        <a href="https://t.me/maktab_bamika" target="_blank">مکتب خصوصی بامیکا</a>
      </p>
      <p>
        <i class="fab fa-facebook"></i> صفحه فیسبوک:
        <a href="https://facebook.com/maktab_bamika" target="_blank">مکتب خصوصی بامیکا</a>
      </p>
    </div>
    <select id="userTypeSelect">
      <option value="admin">مدیر</option>
      <option value="teacher">معلم</option>
      <option value="parent">والدین</option>
    </select>
    <input type="text" id="username" placeholder="نام کاربری" />
    <input type="password" id="password" placeholder="رمز عبور" />
    <button onclick="handleLogin()">ورود</button>
  </div>

  <div class="admin-panel hidden" id="admin-panel">
    <h2>پنل مدیریت</h2>
    <h3>افزودن معلم</h3>
    <input type="text" id="teacherUser" placeholder="نام کاربری معلم" />
    <input type="password" id="teacherPass" placeholder="رمز عبور معلم" />
    <button onclick="registerSpecificUser('teacher')">ثبت معلم</button>
    <div id="teacherList" class="user-list"></div>

    <h3>افزودن والد</h3>
    <input type="text" id="parentUser" placeholder="نام کاربری والد" />
    <input type="password" id="parentPass" placeholder="رمز عبور والد" />
    <button onclick="registerSpecificUser('parent')">ثبت والد</button>
    <div id="parentList" class="user-list"></div>

    <button onclick="logout()">خروج</button>
  </div>

  <div class="teacher-panel hidden" id="teacher-panel">
    <h2>پنل معلم</h2>
    <input type="text" id="studentName" placeholder="نام شاگرد" />
    <input type="text" id="studentFather" placeholder="نام پدر شاگرد" />
    <select id="grade">
      <option disabled selected>انتخاب صنف</option>
      <script>
        for (let i = 1; i <= 10; i++) {
          document.write(
            `<option value="${i}الف">صنف ${i} الف</option><option value="${i}ب">صنف ${i} ب</option>`
          );
        }
      </script>
    </select>
    <input type="text" id="subject" placeholder="مضمون" />
    <select id="performance">
      <option value="عالی">عالی</option>
      <option value="متوسط">متوسط</option>
      <option value="ضعیف">ضعیف</option>
    </select>
    <textarea id="extraNote" placeholder="توضیحات اضافی"></textarea>
    <input type="date" id="recordDate" />
    <button onclick="submitStudentData()">ثبت آمار</button>
    <div id="teacherRecords"></div>
    <button onclick="logout()">خروج</button>
  </div>

  <div class="parent-panel hidden" id="parent-panel">
    <h2>پنل والدین</h2>
    <div id="studentInfo"></div>
    <button onclick="logout()">خروج</button>
  </div>

  <script>
    let users = JSON.parse(localStorage.getItem('users')) || {
      admin: { مدیر: '1234' },
      teacher: {},
      parent: {},
    };
    let studentRecords = JSON.parse(localStorage.getItem('records')) || [];
    let currentUser = null;
    let currentRole = null;

    function saveData() {
      localStorage.setItem('users', JSON.stringify(users));
      localStorage.setItem('records', JSON.stringify(studentRecords));
    }

    function handleLogin() {
      const username = document.getElementById('username').value.trim();
      const password = document.getElementById('password').value.trim();
      const userType = document.getElementById('userTypeSelect').value;
      if (users[userType][username] === password) {
        currentUser = username;
        currentRole = userType;
        document.getElementById('login-panel').classList.add('hidden');
        document.getElementById(`${userType}-panel`).classList.remove('hidden');
        if (userType === 'parent') showStudentInfo();
        if (userType === 'teacher') showTeacherRecords();
        if (userType === 'admin') showUserLists();
      } else {
        alert('اطلاعات ورود نادرست است.');
      }
    }

    function registerSpecificUser(role) {
      const username = document.getElementById(`${role}User`).value.trim();
      const password = document.getElementById(`${role}Pass`).value.trim();
      if (!username || !password) return alert('تمام فیلدها الزامی است.');
      users[role][username] = password;
      saveData();
      document.getElementById(`${role}User`).value = '';
      document.getElementById(`${role}Pass`).value = '';
      alert('کاربر با موفقیت ثبت شد.');
      showUserLists();
    }

    function showUserLists() {
      ['teacher', 'parent'].forEach((role) => {
        const div = document.getElementById(role + 'List');
        div.innerHTML = Object.entries(users[role])
          .map(
            ([user, pass]) => `
          <div class="user-item">
            <input value="${user}" data-role="${role}" data-field="user" />
            <input value="${pass}" data-role="${role}" data-user="${user}" data-field="pass" />
            <button onclick="updateUser(this)">ویرایش</button>
          </div>
        `
          )
          .join('');
      });
    }

    function updateUser(btn) {
      const container = btn.parentElement;
      const usernameInput = container.querySelector('input[data-field="user"]');
      const passwordInput = container.querySelector('input[data-field="pass"]');
      const oldUser = passwordInput.getAttribute('data-user');
      const role = usernameInput.getAttribute('data-role');
      const newUser = usernameInput.value.trim();
      const newPass = passwordInput.value.trim();
      if (!newUser || !newPass) return alert('فیلدها نمی‌توانند خالی باشند.');
      // حذف کاربر قدیمی و اضافه کاربر جدید
      if (oldUser !== newUser) {
        delete users[role][oldUser];
      }
      users[role][newUser] = newPass;
      saveData();
      alert('اطلاعات کاربر بروز شد.');
      showUserLists();
    }

    function submitStudentData() {
      const name = document.getElementById('studentName').value.trim();
      const father = document.getElementById('studentFather').value.trim();
      const grade = document.getElementById('grade').value;
      const subject = document.getElementById('subject').value.trim();
      const performance = document.getElementById('performance').value;
      const note = document.getElementById('extraNote').value.trim();
      const date = document.getElementById('recordDate').value;
      if (!name || !father || !grade || !subject || !performance || !date) {
        return alert('لطفا تمام فیلدهای ضروری را پر کنید.');
      }
      studentRecords.push({ name, father, grade, subject, performance, note, date });
      saveData();
      alert('اطلاعات شاگرد ثبت شد.');
      // پاک کردن فرم
      document.getElementById('studentName').value = '';
      document.getElementById('studentFather').value = '';
      document.getElementById('grade').value = '';
      document.getElementById('subject').value = '';
      document.getElementById('performance').value = 'عالی';
      document.getElementById('extraNote').value = '';
      document.getElementById('recordDate').value = '';
      showTeacherRecords();
    }

    function showTeacherRecords() {
      const container = document.getElementById('teacherRecords');
      if (studentRecords.length === 0) {
        container.innerHTML = '<p>هیچ رکوردی ثبت نشده است.</p>';
        return;
      }
      container.innerHTML = studentRecords
        .map(
          (r) => `
          <div class="record">
            <div><b>نام شاگرد:</b> ${r.name}</div>
            <div><b>نام پدر:</b> ${r.father}</div>
            <div><b>صنف:</b> ${r.grade}</div>
            <div><b>مضمون:</b> ${r.subject}</div>
            <div><b>عملکرد:</b> ${r.performance}</div>
            <div><b>توضیحات:</b> ${r.note || 'ندارد'}</div>
            <div><b>تاریخ ثبت:</b> ${r.date}</div>
          </div>
        `
        )
        .join('');
    }

    function showStudentInfo() {
      const container = document.getElementById('studentInfo');
      if (studentRecords.length === 0) {
        container.innerHTML = '<p>هیچ رکوردی ثبت نشده است.</p>';
        return;
      }
      // نمایش تمام اطلاعات با استایل مشابه
      container.innerHTML = studentRecords
        .map(
          (r) => `
          <div class="record">
            <div><b>نام شاگرد:</b> ${r.name}</div>
            <div><b>نام پدر:</b> ${r.father}</div>
            <div><b>صنف:</b> ${r.grade}</div>
            <div><b>مضمون:</b> ${r.subject}</div>
            <div><b>عملکرد:</b> ${r.performance}</div>
            <div><b>توضیحات:</b> ${r.note || 'ندارد'}</div>
            <div><b>تاریخ ثبت:</b> ${r.date}</div>
          </div>
        `
        )
        .join('');
    }

    function logout() {
      currentUser = null;
      currentRole = null;
      document.getElementById('login-panel').classList.remove('hidden');
      ['admin', 'teacher', 'parent'].forEach((role) =>
        document.getElementById(`${role}-panel`).classList.add('hidden')
      );
      document.getElementById('username').value = '';
      document.getElementById('password').value = '';
    }
  </script>
</body>
</html>
