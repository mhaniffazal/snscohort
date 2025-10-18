# <!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8"/>
  <meta name="viewport" content="width=device-width,initial-scale=1"/>
  <title>CohortX FloorWing — HTML Prototype</title>
  <style>
    :root {
      --sns-yellow: #FFD600;
      --dark-bg: #0A0A0A;
      --card-bg: rgba(20, 20, 20, 0.95);
      --muted: #666;
      --text: #fff;
      --glow: 0 0 20px rgba(255, 214, 0, 0.3);
      --neon: 0 0 10px rgba(255, 214, 0, 0.5), 0 0 20px rgba(255, 214, 0, 0.3), 0 0 30px rgba(255, 214, 0, 0.1);
    }
    * {
      box-sizing: border-box;
      font-family: 'Rajdhani', 'Orbitron', system-ui, sans-serif;
    }
    @keyframes float {
      0% { transform: translateY(0px) rotate(0deg); }
      50% { transform: translateY(-10px) rotate(2deg); }
      100% { transform: translateY(0px) rotate(0deg); }
    }
    @keyframes pulse {
      0% { transform: scale(1); box-shadow: var(--glow); }
      50% { transform: scale(1.05); box-shadow: var(--neon); }
      100% { transform: scale(1); box-shadow: var(--glow); }
    }
    @keyframes bgShift {
      0% { background-position: 0% 0%; }
      50% { background-position: 100% 100%; }
      100% { background-position: 0% 0%; }
    }
    @keyframes glitch {
      0% { clip-path: inset(50% 0 30% 0); }
      20% { clip-path: inset(20% 0 60% 0); }
      40% { clip-path: inset(40% 0 40% 0); }
      60% { clip-path: inset(80% 0 5% 0); }
      80% { clip-path: inset(10% 0 85% 0); }
      100% { clip-path: inset(40% 0 50% 0); }
    }
    body {
      margin: 0;
      min-height: 100vh;
      color: var(--text);
      background: var(--dark-bg);
      background-image: 
        radial-gradient(circle at 50% 50%, rgba(255, 214, 0, 0.1) 0%, transparent 50%),
        linear-gradient(45deg, rgba(255, 214, 0, 0.05) 25%, transparent 25%),
        linear-gradient(-45deg, rgba(255, 214, 0, 0.05) 25%, transparent 25%);
      background-size: 100% 100%, 20px 20px, 20px 20px;
      position: relative;
      overflow-x: hidden;
      animation: bgShift 20s ease infinite;
    }
    body::before {
      content: "";
      position: fixed;
      top: 0;
      left: 0;
      width: 100vw;
      height: 100vh;
      z-index: -1;
      background: 
        repeating-linear-gradient(
          0deg,
          rgba(255, 214, 0, 0.1) 0px,
          rgba(255, 214, 0, 0.1) 1px,
          transparent 1px,
          transparent 2px
        );
      opacity: 0.5;
      pointer-events: none;
    }
    .header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 28px;
      padding: 32px;
      font-size: 1.35rem;
      position: relative;
      z-index: 1;
    }
    .brand {
      display: flex;
      gap: 20px;
      align-items: center;
      animation: float 6s ease-in-out infinite;
    }
    .logo {
      width: 60px;
      height: 60px;
      border-radius: 12px;
      background: var(--sns-yellow);
      display: flex;
      align-items: center;
      justify-content: center;
      font-weight: 700;
      position: relative;
      box-shadow: var(--glow);
      animation: pulse 3s ease-in-out infinite;
    }
    .logo::after {
      content: '';
      position: absolute;
      inset: -2px;
      border: 2px solid var(--sns-yellow);
      border-radius: inherit;
      opacity: 0.5;
      animation: pulse 3s ease-in-out infinite;
    }
    .card {
      background: var(--card-bg);
      border-radius: 15px;
      padding: 25px;
      border: 1px solid rgba(255, 214, 0, 0.1);
      box-shadow: 0 8px 32px rgba(0, 0, 0, 0.5);
      backdrop-filter: blur(10px);
      transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
    }
    .card:hover {
      transform: translateY(-5px) scale(1.02);
      border-color: var(--sns-yellow);
      box-shadow: var(--neon);
    }
    .grid { display: grid; gap: 20px; }
    .grid-3 { grid-template-columns: repeat(3, 1fr); }
    .btn {
      padding: 12px 24px;
      border-radius: 8px;
      border: 2px solid var(--sns-yellow);
      background: transparent;
      color: var(--sns-yellow);
      cursor: pointer;
      font-weight: 600;
      text-transform: uppercase;
      letter-spacing: 1px;
      position: relative;
      overflow: hidden;
      transition: all 0.3s ease;
    }
    .btn::before {
      content: '';
      position: absolute;
      top: 50%;
      left: 50%;
      width: 150%;
      height: 150%;
      background: var(--sns-yellow);
      transform: translate(-50%, -50%) rotate(45deg) translateY(100%);
      transition: all 0.3s ease;
      z-index: -1;
    }
    .btn:hover {
      color: var(--dark-bg);
      box-shadow: var(--neon);
    }
    .btn:hover::before {
      transform: translate(-50%, -50%) rotate(45deg) translateY(0);
    }
    .btn-yellow {
      background: var(--sns-yellow);
      color: var(--dark-bg);
      border: none;
      box-shadow: var(--glow);
    }
    .task {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 20px;
      border-radius: 12px;
      background: rgba(30, 30, 30, 0.9);
      border: 1px solid rgba(255, 214, 0, 0.2);
      transition: all 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
      position: relative;
      overflow: hidden;
    }
    .task::before {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      width: 2px;
      height: 100%;
      background: var(--sns-yellow);
      transform: scaleY(0);
      transition: transform 0.3s ease;
    }
    .task:hover {
      transform: translateX(10px);
      border-color: var(--sns-yellow);
      box-shadow: var(--glow);
    }
    .task:hover::before {
      transform: scaleY(1);
    }
    .task + .task { margin-top: 15px; }
    input, select, textarea {
      padding: 15px;
      border-radius: 8px;
      border: 2px solid rgba(255, 214, 0, 0.2);
      background: rgba(20, 20, 20, 0.8);
      color: var(--text);
      width: 100%;
      transition: all 0.3s ease;
    }
    input:focus, select:focus, textarea:focus {
      outline: none;
      border-color: var(--sns-yellow);
      box-shadow: var(--glow);
    }
    label {
      font-weight: 600;
      font-size: 0.95rem;
      color: var(--text);
      text-transform: uppercase;
      letter-spacing: 1px;
    }
    .link {
      background: transparent;
      border: 2px solid var(--sns-yellow);
      color: var(--sns-yellow);
      padding: 8px 16px;
      border-radius: 8px;
      cursor: pointer;
      transition: all 0.3s ease;
      text-transform: uppercase;
      letter-spacing: 1px;
    }
    .link:hover {
      background: var(--sns-yellow);
      color: var(--dark-bg);
      box-shadow: var(--neon);
    }
    .badge {
      background: rgba(255, 214, 0, 0.1);
      color: var(--sns-yellow);
      padding: 8px 16px;
      border-radius: 20px;
      font-weight: 500;
      text-transform: uppercase;
      letter-spacing: 1px;
    }
    .leader-item {
      display: flex;
      justify-content: space-between;
      padding: 20px;
      border-radius: 12px;
      background: rgba(30, 30, 30, 0.9);
      border: 1px solid rgba(255, 214, 0, 0.2);
      transition: all 0.3s ease;
    }
    .leader-item:hover {
      transform: scale(1.02);
      border-color: var(--sns-yellow);
      box-shadow: var(--neon);
    }
    .muted { color: var(--muted); }
    .small { font-size: 0.88rem; color: var(--muted); }
    .footer {
      margin-top: 32px;
      color: var(--muted);
      font-size: 1.15rem;
      padding: 32px;
      text-align: center;
      position: relative;
    }
    .footer::before {
      content: '';
      position: absolute;
      top: 0;
      left: 50%;
      transform: translateX(-50%);
      width: 100px;
      height: 2px;
      background: var(--sns-yellow);
      box-shadow: var(--glow);
    }
    .pill {
      display: inline-block;
      padding: 8px 16px;
      border-radius: 20px;
      background: rgba(255, 214, 0, 0.1);
      color: var(--sns-yellow);
      border: 1px solid rgba(255, 214, 0, 0.2);
      margin-right: 8px;
      transition: all 0.3s ease;
      text-transform: uppercase;
      letter-spacing: 1px;
    }
    .pill:hover {
      transform: translateY(-2px);
      background: rgba(255, 214, 0, 0.2);
      box-shadow: var(--neon);
    }
  </style>
</head>
<body>
  <div class="wrap">
    <div class="header">
      <div class="brand">
        <div class="logo"><img 
        <div>
          <div style="font-weight:800;font-size:1.15rem">CohortX FloorWing</div>
          <div class="muted">Design Thinking Cohort Managment Portal</div>
        </div>
      </div>
      <div class="topbar">
        <button class="link" onclick="resetData()">Reset Data</button>
        <div id="loggedAs" class="small muted">Not signed in</div>
      </div>
    </div>

    <div id="app"></div>

    <div class="footer">
      Tip: this prototype stores data in your browser (localStorage). Use Reset Data to restore the initial demo data.
    </div>
  </div>

<script>
/* =========================
   Simple Single-file App
   =========================
   Features:
   - 4-role login (student, mentor, administrator, floorwing)
   - localStorage "cohortx_state" persistence
   - Student can mark tasks done and upload proof (mock)
   - Mentor can create tasks and assign to students
   - Admin can add users
   - Floorwing sees students on their floor
*/

/* ---------- default demo state ---------- */
const defaultState = {
  users: [
    { id: "s1", name: "Mohamed Hanif", role: "student", floor: "2", points: 100, username: "student1", password: "pass1", attendance: 90 },
    { id: "s2", name: "Narthika", role: "student", floor: "2", points: 2497, username: "student2", password: "pass2", attendance: 95 },
    { id: "s3", name: "Sharvesh", role: "student", floor: "3", points: 2214, username: "student3", password: "pass3", attendance: 88 },
    { id: "m1", name: "Mr. Hariharan (Mentor)", role: "mentor", floor: "2", points: 0, username: "mentor1", password: "mentorpass" },
    { id: "f2", name: "Mr. Floorwing 2", role: "floorwing", floor: "2", points: 0, username: "floorwing2", password: "floorpass" },
    { id: "a1", name: "Administrator", role: "admin", points: 0, username: "admin1", password: "adminpass" }
  ],
  tasks: [
    { id: "t1", title: "Complete Databricks Course", pillar: "SCD", assignedTo: "s1", points: 30, status: "assigned", uploaderProofUrl: null, createdBy: "m1", reviewStatus: null },
    { id: "t2", title: "LinkedIn Post x2", pillar: "SCD", assignedTo: "s2", points: 20, status: "assigned", uploaderProofUrl: null, createdBy: "m1", reviewStatus: null }
  ],
  announcements: [
    { id: "a1", title: "Welcome to CohortX!", content: "Kickoff meeting at 10am tomorrow.", createdBy: "m1", date: "2025-10-01" }
  ],
  feedback: [],
  pillars: ["CLT","SCD","CFC","IIPC","SRI"]
};

/* ---------- storage helpers ---------- */
function initMockData() {
  if (!localStorage.getItem("cohortx_state")) {
    localStorage.setItem("cohortx_state", JSON.stringify(defaultState));
  }
}
function readState(){ return JSON.parse(localStorage.getItem("cohortx_state")); }
function writeState(s){ localStorage.setItem("cohortx_state", JSON.stringify(s)); }
function setCurrentUser(user){ localStorage.setItem("cohortx_user", JSON.stringify(user)); updateLoggedAs(); }
function getCurrentUser(){ return JSON.parse(localStorage.getItem("cohortx_user")); }
function clearCurrentUser(){ localStorage.removeItem("cohortx_user"); updateLoggedAs(); }

/* ---------- small helpers ---------- */
function id(prefix="id"){ return prefix+Date.now().toString(36).slice(6) + Math.floor(Math.random()*100) }
function q(html){ const div=document.createElement('div'); div.innerHTML=html.trim(); return div.firstChild; }
function updateLoggedAs(){
  const u = getCurrentUser();
  document.getElementById("loggedAs").textContent = u ? "Signed in as " + u.name + " (" + u.role + ")" : "Not signed in";
}

/* ---------- app render logic ---------- */
function render() {
  const user = getCurrentUser();
  if (!user) return renderLogin();
  if (user.role === "student") return renderStudentDashboard();
  if (user.role === "mentor") return renderMentorDashboard();
  if (user.role === "admin") return renderAdminDashboard();
  if (user.role === "floorwing") return renderFloorwingDashboard();
  renderLogin();
}

/* ---------- login page ---------- */
function renderLogin(){
  initMockData();
  clearCurrentUser();
  var html = `
    <div class="card" style="text-align:center;max-width:400px;margin:auto">
      <h1 style="margin:0 0 18px 0;font-size:2.2rem">CohortX Portal Login</h1>
      <form id="loginForm" style="margin-bottom:18px">
        <input name="username" placeholder="Username" required style="margin-bottom:8px" />
        <input name="password" type="password" placeholder="Password" required style="margin-bottom:8px" />
        <button class="btn btn-yellow" type="submit">Login</button>
      </form>
      <div class="muted" style="margin-bottom:12px">Demo credentials:<br>
        <b>Student:</b> student1 / pass1<br>
        <b>Mentor:</b> mentor1 / mentorpass<br>
        <b>Admin:</b> admin1 / adminpass<br>
        <b>Floorwing:</b> floorwing2 / floorpass
      </div>
      <div style="margin-top:12px" class="small muted">Click Reset Data (top-right) to restore demo data anytime.</div>
    </div>
  `;
  document.getElementById("app").innerHTML = html;
  updateLoggedAs();
  document.getElementById("loginForm").onsubmit = function(e){
    e.preventDefault();
    const f = e.target;
    loginWithCredentials(f.username.value, f.password.value);
  };
}

/* ---------- login function (choose first user of role) ---------- */
function loginWithCredentials(username, password){
  initMockData();
  const state = readState();
  const user = state.users.find(function(u){ return u.username===username && u.password===password; });
  if(user){
    setCurrentUser(user);
    render();
  } else {
    alert("Invalid credentials. Please try again.");
  }
}

/* ---------- logout ---------- */
function logout(){
  clearCurrentUser();
  renderLogin();
}

/* ---------- Student dashboard ---------- */
function renderStudentDashboard(){
  const state = readState();
  const current = getCurrentUser();
  // refresh user object from state (to get latest points)
  const me = state.users.find(function(u){ return u.id===current.id; }) || current;
  const myTasks = state.tasks.filter(function(t){ return t.assignedTo===me.id; });

  let html = '';
  // Profile & Progress
  html += '<div style="display:flex;gap:12px;align-items:center;margin-bottom:12px">';
  html += '<div style="flex:1" class="card">';
  html += '<div class="small muted">Name</div>';
  html += '<div style="font-weight:800">' + me.name + '</div>';
  html += '<div style="margin-top:10px" class="small muted">Points</div>';
  html += '<div style="font-size:24px;font-weight:800">' + me.points + '</div>';
  html += '<div style="margin-top:10px" class="small muted">Attendance</div>';
  html += '<div style="font-size:18px;font-weight:700">' + (me.attendance || 0) + '%</div>';
  html += '<div style="margin-top:8px"><button class="link" onclick="logout()">Logout</button></div>';
  html += '</div>';
  html += '<div style="flex:2" class="card">';
  html += '<div style="display:flex;justify-content:space-between;align-items:center;margin-bottom:8px">';
  html += '<div><strong>Student Report</strong> <span class="small muted">• Progress graph</span></div>';
  html += '<div class="pill">Floor ' + (me.floor || '-') + '</div>';
  html += '</div>';
  // Simple progress bar (mock)
  html += '<div style="margin:12px 0">';
  html += '<div class="small muted">Monthly Points</div>';
  html += '<div style="background:#eee;border-radius:8px;height:18px;width:100%;overflow:hidden;margin-bottom:6px">';
  html += '<div style="background:linear-gradient(90deg,#FFD600,#ffeab0);height:100%;width:' + Math.min(100, me.points/30) + '%"></div>';
  html += '</div>';
  html += '<div class="small muted">Completed Tasks: ' + myTasks.filter(function(t){ return t.status==='done'; }).length + '</div>';
  html += '</div>';
  html += '</div>';
  html += '</div>';
  // Announcements
  html += '<div class="card" style="margin-bottom:12px">';
  html += '<div style="font-weight:700;margin-bottom:8px">Announcements</div>';
  if (state.announcements && state.announcements.length > 0) {
    html += state.announcements.slice(-5).reverse().map(function(a){ return '<div style="margin-bottom:8px"><strong>' + a.title + '</strong><div class="small muted">' + a.content + ' <span style="float:right">' + a.date + '</span></div></div>'; }).join('');
  } else {
    html += '<div class="muted">No announcements yet.</div>';
  }
  html += '</div>';
  // Tasks
  html += '<div class="card" style="margin-bottom:12px">';
  html += '<div style="font-weight:700;margin-bottom:8px">My Tasks</div>';
  if (myTasks.length === 0) {
    html += '<div class="muted">No tasks assigned yet.</div>';
  } else {
    html += myTasks.map(function(t){ return renderTaskRow(t, me); }).join("");
  }
  html += '</div>';
  // Feedback/Grievances
  html += '<div class="card" style="margin-bottom:12px">';
  html += '<div style="font-weight:700;margin-bottom:8px">Feedback / Grievances</div>';
  html += '<form id="feedbackForm"><textarea name="feedback" rows="2" style="width:100%;border-radius:8px;padding:8px;margin-bottom:8px" placeholder="Type your feedback or grievance..."></textarea><button class="btn btn-yellow" type="submit">Submit</button></form>';
  html += '<div id="feedbackList" style="margin-top:10px">';
  if (state.feedback && state.feedback.filter(function(f){ return f.userId===me.id; }).length > 0) {
    html += state.feedback.filter(function(f){ return f.userId===me.id; }).slice(-5).reverse().map(function(f){ return '<div class="small muted" style="margin-bottom:6px">' + f.text + ' <span style="float:right">' + f.date + '</span></div>'; }).join('');
  }
  html += '</div>';
  html += '</div>';
  // Leaderboard
  html += '<div class="card" style="margin-top:12px">';
  html += '<div style="font-weight:700;margin-bottom:8px">Leaderboard (Top Students)</div>';
  html += state.users.filter(function(u){ return u.role==='student'; }).sort(function(a,b){return b.points-a.points;}).slice(0,6).map(function(u){
    return '<div class="leader-item" style="margin-top:8px"><div><strong>' + u.name + '</strong><div class="small muted">Floor: ' + (u.floor||'-') + '</div></div><div style="font-weight:700">' + u.points + '</div></div>';
  }).join('');
  html += '</div>';

  document.getElementById("app").innerHTML = html;
  updateLoggedAs();

  // Feedback form submit
  var feedbackForm = document.getElementById("feedbackForm");
  if (feedbackForm) {
    feedbackForm.onsubmit = function(e){
      e.preventDefault();
      var f = e.target;
      var text = f.feedback.value.trim();
      if (!text) return;
      var state = readState();
      state.feedback = state.feedback || [];
      state.feedback.push({ userId: me.id, text: text, date: new Date().toISOString().slice(0,10) });
      writeState(state);
      renderStudentDashboard();
    };
  }
}

/* ---------- Mentor dashboard ---------- */
function renderMentorDashboard(){
  const state = readState();
  const current = getCurrentUser();

  var html = '';
  html += '<div style="display:grid;grid-template-columns:320px 1fr;gap:12px">';
  
  // Left column: Create Task, Post Announcement, Update Attendance
  html += '<div>';
  
  // Create Task
  html += '<div class="card" style="margin-bottom:12px">';
  html += '<div style="font-weight:700;margin-bottom:8px">Create Task</div>';
  html += '<form id="createTaskForm">';
  html += '<label>Title</label><input name="title" required />';
  html += '<label style="margin-top:8px">Pillar</label>';
  html += '<select name="pillar">' + state.pillars.map(function(p){return '<option>' + p + '</option>';}).join('') + '</select>';
  html += '<label style="margin-top:8px">Assign to (student id)</label>';
  html += '<input name="assignedTo" placeholder="e.g., s1" required />';
  html += '<label style="margin-top:8px">Points</label><input name="points" type="number" value="10" />';
  html += '<div style="margin-top:8px"><button class="btn btn-yellow" type="submit">Add Task</button></div>';
  html += '</form>';
  html += '<div style="margin-top:10px" class="small muted">Tip: use student id shown in Admin -> Members to assign tasks.</div>';
  html += '</div>';

  // Post Announcement
  html += '<div class="card" style="margin-bottom:12px">';
  html += '<div style="font-weight:700;margin-bottom:8px">Post Announcement</div>';
  html += '<form id="announcementForm">';
  html += '<label>Title</label><input name="title" required />';
  html += '<label style="margin-top:8px">Content</label><textarea name="content" rows="2" required></textarea>';
  html += '<div style="margin-top:8px"><button class="btn btn-yellow" type="submit">Post</button></div>';
  html += '</form>';
  html += '</div>';

  // Update Attendance
  html += '<div class="card">';
  html += '<div style="font-weight:700;margin-bottom:8px">Update Attendance</div>';
  html += '<form id="attendanceForm">';
  html += '<label>Student ID</label><input name="studentId" placeholder="e.g., s1" required />';
  html += '<label style="margin-top:8px">New Attendance %</label><input name="attendance" type="number" min="0" max="100" required />';
  html += '<div style="margin-top:8px"><button class="btn btn-yellow" type="submit">Update</button></div>';
  html += '</form>';
  html += '</div>';

  html += '</div>';

  // Right column: All tasks
  html += '<div class="card">';
  html += '<div style="display:flex;justify-content:space-between;align-items:center">';
  html += '<div style="font-weight:700">All Tasks (for Review)</div>';
  html += '<div><button class="link" onclick="logout()">Logout</button></div>';
  html += '</div>';
  html += '<div id="tasksList" style="margin-top:10px">';
  if (state.tasks.length === 0) {
    html += '<div class="muted">No tasks</div>';
  } else {
    html += state.tasks.sort(function(a,b){ return (a.status==='submitted' ? -1 : 1); }).map(function(t){return renderTaskRow(t, current);}).join('');
  }
  html += '</div>';
  html += '</div>';

  html += '</div>';

  document.getElementById("app").innerHTML = html;
  updateLoggedAs();

  // form submit handlers
  document.getElementById("createTaskForm").onsubmit = function(e){
    e.preventDefault();
    const f = e.target;
    addTask({
      title: f.title.value,
      pillar: f.pillar.value,
      assignedTo: f.assignedTo.value,
      points: Number(f.points.value) || 10,
      createdBy: current.id
    });
    f.reset();
    renderMentorDashboard();
  };
  document.getElementById("announcementForm").onsubmit = function(e){
    e.preventDefault();
    const f = e.target;
    addAnnouncement({ title: f.title.value, content: f.content.value, createdBy: current.id });
    f.reset();
    renderMentorDashboard();
  };
  document.getElementById("attendanceForm").onsubmit = function(e){
    e.preventDefault();
    const f = e.target;
    updateAttendance(f.studentId.value, f.attendance.value);
    f.reset();
    renderMentorDashboard();
  };
}

/* ---------- Admin dashboard ---------- */
function renderAdminDashboard(){
  const state = readState();
  var html = '';
  html += '<div style="display:grid;grid-template-columns:320px 1fr;gap:12px">';
  html += '<div class="card">';
  html += '<div style="font-weight:700;margin-bottom:8px">Add Member</div>';
  html += '<form id="addMemberForm">';
  html += '<label>Name</label><input name="name" required />';
  html += '<label style="margin-top:8px">Username</label><input name="username" required />';
  html += '<label style="margin-top:8px">Password</label><input name="password" required />';
  html += '<label style="margin-top:8px">Role</label>';
  html += '<select name="role"><option value="student">Student</option><option value="mentor">Mentor</option><option value="floorwing">FloorWing</option><option value="admin">Administrator</option></select>';
  html += '<label style="margin-top:8px">Floor (optional)</label><input name="floor" placeholder="e.g., 2" />';
  html += '<div style="margin-top:8px"><button class="btn btn-yellow" type="submit">Add Member</button></div>';
  html += '</form>';
  html += '</div>';

  html += '<div class="card">';
  html += '<div style="display:flex;justify-content:space-between;align-items:center">';
  html += '<div style="font-weight:700">Members</div>';
  html += '<div><button class="link" onclick="logout()">Logout</button></div>';
  html += '</div>';
  html += '<div style="margin-top:8px">';
  html += state.users.map(function(u){
    return '<div style="margin-top:8px" class="leader-item"><div><strong>' + u.name + '</strong> ('+u.username+')<div class="small muted">' + u.role + ' • Floor: ' + (u.floor||'-') + '</div></div><div style="text-align:right"><div style="font-weight:700">' + u.points + '</div><div class="small muted">id: ' + u.id + '</div></div></div>';
  }).join('');
  html += '</div>';
  html += '</div>';
  html += '</div>';
  
  document.getElementById("app").innerHTML = html;
  updateLoggedAs();

  document.getElementById("addMemberForm").onsubmit = function(e){
    e.preventDefault();
    const f = e.target;
    addMember({ name: f.name.value, username: f.username.value, password: f.password.value, role: f.role.value, floor: f.floor.value || null });
    f.reset();
    renderAdminDashboard();
  };
}

/* ---------- Floorwing dashboard ---------- */
function renderFloorwingDashboard(){
  const state = readState();
  const current = getCurrentUser();
  const students = state.users.filter(function(u){ return u.role==='student' && u.floor === current.floor; });

  var html = '';
  html += '<div style="display:grid;grid-template-columns:1fr 320px;gap:12px">';
  html += '<div class="card">';
  html += '<div style="display:flex;justify-content:space-between;align-items:center">';
  html += '<div><strong>Floor ' + current.floor + ' Overview</strong><div class="small muted">Students & points</div></div>';
  html += '<div><button class="link" onclick="logout()">Logout</button></div>';
  html += '</div>';
  html += '<div style="margin-top:12px">';
  if (students.length === 0) {
    html += '<div class="muted">No students found on your floor</div>';
  } else {
    html += students.map(function(s){
      return '<div class="leader-item" style="margin-top:8px"><div><strong>' + s.name + '</strong><div class="small muted">id: ' + s.id + '</div></div><div style="font-weight:700">' + s.points + '</div></div>';
    }).join('');
  }
  html += '</div>';
  html += '</div>';

  html += '<div class="card">';
  html += '<div style="font-weight:700">Announcements</div>';
  if (state.announcements && state.announcements.length > 0) {
    html += state.announcements.slice(-5).reverse().map(function(a){ return '<div style="margin-bottom:8px"><strong>' + a.title + '</strong><div class="small muted">' + a.content + ' <span style="float:right">' + a.date + '</span></div></div>'; }).join('');
  } else {
    html += '<div class="muted">No announcements yet.</div>';
  }
  html += '</div>';
  html += '</div>';

  document.getElementById("app").innerHTML = html;
  updateLoggedAs();
}

/* ---------- global operations ---------- */
function addTask({title,pillar,assignedTo,points,createdBy}) {
  const state = readState();
  const t = { id: id("t"), title, pillar, assignedTo, points, status:'assigned', uploaderProofUrl:null, createdBy: createdBy || 'mentor', reviewStatus: null };
  state.tasks.push(t);
  writeState(state);
}
function addMember({name,username,password,role,floor}) {
  const state = readState();
  const u = { id: id(role[0]||'u'), name, username, password, role, floor: floor || null, points:0, attendance: 0 };
  state.users.push(u);
  writeState(state);
}
function addAnnouncement({title, content, createdBy}){
  const state = readState();
  state.announcements = state.announcements || [];
  const a = { id: id('a'), title, content, createdBy, date: new Date().toISOString().slice(0,10) };
  state.announcements.push(a);
  writeState(state);
}
function updateAttendance(studentId, attendance){
  const state = readState();
  const user = state.users.find(function(u){ return u.id === studentId; });
  if(user){
    user.attendance = Number(attendance);
    writeState(state);
  } else {
    alert('Student not found');
  }
}
function approveTask(taskId){
  const state = readState();
  const t = state.tasks.find(function(x){ return x.id===taskId; });
  if(!t) return alert('Task not found');
  t.reviewStatus = 'approved';
  t.status = 'done';
  const user = state.users.find(function(u){ return u.id===t.assignedTo; });
  if(user) user.points += t.points;
  writeState(state);
  render();
}
function rejectTask(taskId){
  const state = readState();
  const t = state.tasks.find(function(x){ return x.id===taskId; });
  if(!t) return alert('Task not found');
  t.reviewStatus = 'rejected';
  t.status = 'assigned'; // reset to assigned
  t.uploaderProofUrl = null; // clear proof
  writeState(state);
  render();
}
function markDone(taskId){
  // This is now effectively deprecated in favor of uploadProof, but kept for now
  const state = readState();
  const t = state.tasks.find(function(x){ return x.id===taskId; });
  if(!t) return alert('Task not found');
  if(t.status === 'done') return alert('Already done');
  t.status = 'submitted'; // Student submits, mentor approves
  writeState(state);
  render();
}
function uploadProof(taskId){
  // mock upload: set URL and status submitted
  const state = readState();
  const t = state.tasks.find(function(x){ return x.id===taskId; });
  if(!t) return alert('Task not found');
  t.uploaderProofUrl = "https://example.com/proof-"+taskId+".png";
  t.status = 'submitted';
  t.reviewStatus = null;
  writeState(state);
  render();
}

/* ---------- UI small render helper for task row ---------- */
function renderTaskRow(task, currentUser){
  var statusBadge = '';
  if (task.reviewStatus === 'approved') {
    statusBadge = '<span class="success" style="padding:6px;border-radius:8px">Approved</span>';
  } else if (task.reviewStatus === 'rejected') {
    statusBadge = '<span class="danger" style="padding:6px;border-radius:8px">Rejected</span>';
  } else if (task.status === 'submitted') {
    statusBadge = '<span class="pill">Pending Review</span>';
  } else if (task.status === 'done') {
    statusBadge = '<span class="success" style="padding:6px;border-radius:8px">Done</span>';
  } else {
    statusBadge = '<span class="small muted">Assigned</span>';
  }

  var uploader = '';
  if (task.uploaderProofUrl) {
    uploader = '<div class="small muted">Proof: <a href="' + task.uploaderProofUrl + '" target="_blank">view</a></div>';
  }

  var controlsStudent = '<div style="display:flex;gap:8px">';
  if (task.status !== 'submitted' && task.status !== 'done' && task.reviewStatus !== 'approved') {
    controlsStudent += '<button class="link" onclick="uploadProof(\'' + task.id + '\')">Upload Proof</button>';
  } else {
    controlsStudent += '<div class="small muted">Awaiting review</div>';
  }
  controlsStudent += '</div>';

  var controlsMentor = '<div style="display:flex;gap:8px">';
  if (task.status === 'submitted') {
    controlsMentor += '<button class="btn" style="background:#c9f3d1" onclick="approveTask(\'' + task.id + '\')">Approve</button>';
    controlsMentor += '<button class="btn" style="background:#ffefef" onclick="rejectTask(\'' + task.id + '\')">Reject</button>';
  } else {
    controlsMentor += '<div class="small muted">Assigned to: ' + task.assignedTo + '</div>';
  }
  controlsMentor += '</div>';

  var rightControls = '';
  if (currentUser.role === 'student') {
    rightControls = controlsStudent;
  } else if (currentUser.role === 'mentor') {
    rightControls = controlsMentor;
  } else {
    rightControls = '<div class="small muted">Points: ' + task.points + '</div>';
  }

  var html = '<div class="task">';
  html += '<div>';
  html += '<div style="font-weight:700">' + task.title + '</div>';
  html += '<div class="small muted">Pillar: ' + task.pillar + ' • Points: ' + task.points + '</div>';
  html += uploader;
  html += '</div>';
  html += '<div style="text-align:right">';
  html += '<div style="margin-bottom:8px">' + statusBadge + '</div>';
  html += '<div>' + rightControls + '</div>';
  html += '</div>';
  html += '</div>';
  return html;
}

/* ---------- reset demo data and re-run ---------- */
function resetData(){
  if(!confirm("Reset demo data? This will erase local changes.")) return;
  localStorage.removeItem("cohortx_state");
  localStorage.removeItem("cohortx_user");
  initMockData();
  renderLogin();
}

/* ---------- start ---------- */
initMockData();
updateLoggedAs();
render();
</script>
</body>
</html>
