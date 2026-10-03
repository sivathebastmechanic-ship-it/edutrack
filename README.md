[edutrack_canvas_web_portal.html](https://github.com/user-attachments/files/33004621/edutrack_canvas_web_portal.html)[Uploading edutra<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>EduTrack - College Attendance & Management Portal</title>
    <style>
        :root {
            --primary: #0056b3;
            --primary-hover: #004085;
            --success: #28a745;
            --danger: #dc3545;
            --warning: #ffc107;
            --info: #17a2b8;
            --bg-light: #f4f6f9;
            --card-bg: #ffffff;
            --text-dark: #2c3e50;
            --text-muted: #6c757d;
            --border-color: #e9ecef;
        }

        * {
            box-sizing: border-box;
            font-family: 'Segoe UI', system-ui, -apple-system, sans-serif;
            margin: 0;
            padding: 0;
        }

        body {
            background-color: var(--bg-light);
            color: var(--text-dark);
            line-height: 1.5;
            padding-bottom: 30px;
        }

        /* Top Header Navigation Bar */
        .navbar {
            background: linear-gradient(135deg, #0056b3, #003366);
            color: white;
            padding: 15px 25px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            box-shadow: 0 4px 12px rgba(0,0,0,0.15);
            flex-wrap: wrap;
            gap: 10px;
        }

        .navbar-brand {
            display: flex;
            align-items: center;
            gap: 10px;
            font-size: 20px;
            font-weight: 700;
        }

        .edit-college-btn {
            background: rgba(255,255,255,0.2);
            color: white;
            border: 1px solid rgba(255,255,255,0.4);
            padding: 7px 14px;
            border-radius: 6px;
            cursor: pointer;
            font-size: 13px;
            font-weight: 600;
            transition: all 0.2s ease;
        }

        .edit-college-btn:hover {
            background: rgba(255,255,255,0.35);
        }

        /* Main Layout Container */
        .container {
            max-width: 1200px;
            margin: 20px auto;
            padding: 0 15px;
        }

        /* Faculty & Term Card */
        .info-card {
            background: var(--card-bg);
            border-radius: 10px;
            padding: 16px 20px;
            display: flex;
            gap: 20px;
            margin-bottom: 20px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.05);
            flex-wrap: wrap;
        }

        .info-group {
            flex: 1;
            min-width: 200px;
        }

        .info-group label {
            display: block;
            font-size: 11px;
            font-weight: 700;
            color: var(--text-muted);
            margin-bottom: 5px;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }

        .info-group input {
            width: 100%;
            padding: 8px 12px;
            border: 1px solid #ccc;
            border-radius: 6px;
            font-size: 14px;
            outline: none;
            background: #fff;
        }

        .info-group input:focus {
            border-color: var(--primary);
            box-shadow: 0 0 0 3px rgba(0, 86, 179, 0.1);
        }

        /* Tab Navigation Bar */
        .tabs {
            display: flex;
            gap: 8px;
            margin-bottom: 20px;
            border-bottom: 2px solid var(--border-color);
            overflow-x: auto;
            white-space: nowrap;
        }

        .tab-btn {
            padding: 12px 20px;
            border: none;
            background: transparent;
            font-size: 14px;
            font-weight: 600;
            color: var(--text-muted);
            cursor: pointer;
            border-bottom: 3px solid transparent;
            transition: all 0.2s ease;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .tab-btn.active {
            color: var(--primary);
            border-bottom-color: var(--primary);
            background: var(--card-bg);
            border-radius: 8px 8px 0 0;
        }

        /* Page Content Views */
        .page-view {
            display: none;
            background: var(--card-bg);
            padding: 25px;
            border-radius: 12px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.05);
        }

        .page-view.active {
            display: block;
        }

        /* Date Range Control Bar (Dashboard) */
        .filter-bar {
            background: #f8f9fa;
            border: 1px solid var(--border-color);
            padding: 15px;
            border-radius: 8px;
            display: flex;
            gap: 15px;
            align-items: center;
            margin-bottom: 20px;
            flex-wrap: wrap;
        }

        .filter-group {
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .filter-group label {
            font-size: 13px;
            font-weight: 600;
            color: var(--text-dark);
        }

        .filter-group select, .filter-group input {
            padding: 7px 10px;
            border: 1px solid #ccc;
            border-radius: 6px;
            font-size: 13px;
        }

        /* Metrics Cards Grid */
        .metrics-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
            gap: 15px;
            margin-bottom: 25px;
        }

        .metric-card {
            background: #f8f9fa;
            border-left: 5px solid var(--primary);
            padding: 16px;
            border-radius: 8px;
            box-shadow: 0 1px 3px rgba(0,0,0,0.05);
        }

        .metric-card.present { border-left-color: var(--success); }
        .metric-card.absent { border-left-color: var(--danger); }
        .metric-card.late { border-left-color: var(--warning); }
        .metric-card.rate { border-left-color: var(--info); }

        .metric-card h3 {
            font-size: 11px;
            color: var(--text-muted);
            text-transform: uppercase;
            margin-bottom: 5px;
            letter-spacing: 0.5px;
        }

        .metric-card p {
            font-size: 26px;
            font-weight: 700;
            color: var(--text-dark);
        }

        /* Charts Layout Section */
        .charts-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
            margin-bottom: 25px;
        }

        @media (max-width: 800px) {
            .charts-container {
                grid-template-columns: 1fr;
            }
        }

        .chart-box {
            background: #ffffff;
            border: 1px solid var(--border-color);
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 2px 6px rgba(0,0,0,0.03);
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        .chart-box h3 {
            font-size: 15px;
            color: var(--primary);
            margin-bottom: 15px;
            width: 100%;
            text-align: left;
            border-bottom: 2px solid #f0f0f0;
            padding-bottom: 8px;
        }

        /* Custom CSS Pie Chart Container & Inner Center Text */
        .pie-chart-wrapper {
            position: relative;
            display: flex;
            justify-content: center;
            align-items: center;
            margin: 10px 0;
        }

        .pie-chart {
            width: 170px;
            height: 170px;
            border-radius: 50%;
            background: conic-gradient(
                var(--success) 0% var(--present-deg, 0%),
                var(--danger) var(--present-deg, 0%) var(--absent-deg, 0%),
                var(--warning) var(--absent-deg, 0%) 100%
            );
            box-shadow: 0 4px 10px rgba(0,0,0,0.1);
            position: relative;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: background 0.3s ease;
        }

        .pie-center-label {
            width: 80px;
            height: 80px;
            background: white;
            border-radius: 50%;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            font-weight: 700;
            box-shadow: inset 0 2px 5px rgba(0,0,0,0.1);
        }

        .pie-center-label .center-pct {
            font-size: 18px;
            color: var(--primary);
        }

        .pie-center-label .center-title {
            font-size: 9px;
            color: var(--text-muted);
            text-transform: uppercase;
        }

        .chart-legend {
            display: flex;
            flex-direction: column;
            gap: 8px;
            width: 100%;
            margin-top: 15px;
        }

        .legend-row {
            display: flex;
            justify-content: space-between;
            align-items: center;
            background: #f8f9fa;
            padding: 8px 12px;
            border-radius: 6px;
            font-size: 12px;
            font-weight: 600;
        }

        .legend-item {
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .legend-dot {
            width: 12px;
            height: 12px;
            border-radius: 50%;
        }

        .pie-pct-badge {
            padding: 2px 8px;
            border-radius: 12px;
            color: white;
            font-size: 11px;
            font-weight: 700;
        }

        /* Bar Chart with Percentages */
        .bar-chart {
            width: 100%;
            display: flex;
            flex-direction: column;
            gap: 14px;
            margin-top: 10px;
        }

        .bar-item {
            display: flex;
            flex-direction: column;
            gap: 6px;
        }

        .bar-label {
            display: flex;
            justify-content: space-between;
            align-items: center;
            font-size: 13px;
            font-weight: 600;
        }

        .pct-badge {
            background: var(--text-dark);
            color: white;
            padding: 2px 8px;
            border-radius: 12px;
            font-size: 11px;
            font-weight: 700;
        }

        .bar-track {
            width: 100%;
            height: 12px;
            background: #e9ecef;
            border-radius: 6px;
            overflow: hidden;
        }

        .bar-fill {
            height: 100%;
            background: linear-gradient(90deg, #0056b3, #17a2b8);
            border-radius: 6px;
            transition: width 0.4s ease;
        }

        /* Responsive Attendance Table */
        .table-responsive {
            width: 100%;
            overflow-x: auto;
            margin-top: 15px;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            min-width: 700px;
        }

        th, td {
            padding: 12px 14px;
            text-align: left;
            border-bottom: 1px solid var(--border-color);
            font-size: 13px;
        }

        th {
            background-color: #f8f9fa;
            color: #555;
            font-size: 12px;
            text-transform: uppercase;
        }

        /* Status Action Buttons */
        .status-btn-group {
            display: flex;
            gap: 4px;
            flex-wrap: wrap;
        }

        .status-btn {
            padding: 5px 9px;
            border: 1px solid #ccc;
            background: #fff;
            border-radius: 4px;
            cursor: pointer;
            font-weight: 600;
            font-size: 11px;
            transition: all 0.2s ease;
        }

        .status-btn.present-btn.active { background: var(--success); color: white; border-color: var(--success); }
        .status-btn.absent-btn.active { background: var(--danger); color: white; border-color: var(--danger); }
        .status-btn.late-btn.active { background: var(--warning); color: #333; border-color: var(--warning); }
        .status-btn.excused-btn.active { background: var(--info); color: white; border-color: var(--info); }

        /* General Action Buttons */
        .btn-main {
            background: var(--primary);
            color: white;
            border: none;
            padding: 9px 16px;
            border-radius: 6px;
            font-size: 13px;
            font-weight: 600;
            cursor: pointer;
            transition: background 0.2s;
        }

        .btn-main:hover { background: var(--primary-hover); }
        .btn-success { background: var(--success); }
        .btn-success:hover { background: #218838; }

        .action-bar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
            flex-wrap: wrap;
            gap: 10px;
        }

        /* Add Student Form Layout */
        .form-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 18px;
        }

        .form-group {
            margin-bottom: 10px;
        }

        .form-group label {
            display: block;
            font-weight: 600;
            font-size: 13px;
            margin-bottom: 6px;
        }

        .form-group input, .form-group select {
            width: 100%;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 6px;
            font-size: 14px;
            outline: none;
        }

        .form-group input:focus, .form-group select:focus {
            border-color: var(--primary);
        }

        .search-box {
            padding: 8px 12px;
            border: 1px solid #ccc;
            border-radius: 6px;
            width: 250px;
            font-size: 13px;
        }
    </style>
</head>
<body>

    <!-- Header Navbar -->
    <div class="navbar">
        <div class="navbar-brand">
            <span id="displayCollegeName">🏛️ Anna University - Attendance Portal</span>
        </div>
        <button class="edit-college-btn" onclick="editCollegeName()">✏️ Edit College Name</button>
    </div>

    <div class="container">
        
        <!-- Editable Faculty Info Bar -->
        <div class="info-card">
            <div class="info-group">
                <label>Faculty / Teacher Name (Editable)</label>
                <input type="text" id="teacherName" value="Sivaraman R">
            </div>
            <div class="info-group">
                <label>Academic Term / Session</label>
                <input type="text" id="termDetails" value="Term 2026-Q3">
            </div>
        </div>

        <!-- Navigation Tabs -->
        <div class="tabs">
            <button class="tab-btn active" onclick="switchTab('dashboardView', this)">📊 Dashboard Analytics</button>
            <button class="tab-btn" onclick="switchTab('attendanceView', this)">📝 Attendance Entry</button>
            <button class="tab-btn" onclick="switchTab('addStudentView', this)">➕ Add Student Page</button>
        </div>

        <!-- 1. DASHBOARD VIEW -->
        <div id="dashboardView" class="page-view active">
            
            <!-- Date Filter Bar -->
            <div class="filter-bar">
                <div class="filter-group">
                    <label>View Mode:</label>
                    <select id="viewModeSelect" onchange="handleFilterChange()">
                        <option value="daily">Daily View</option>
                        <option value="monthly">Monthly View</option>
                        <option value="yearly">Yearly View</option>
                    </select>
                </div>

                <div class="filter-group" id="datePickerGroup">
                    <label>Select Date:</label>
                    <input type="date" id="selectedDate" value="2026-10-03" onchange="updateMetrics()">
                </div>

                <div class="filter-group" id="monthPickerGroup" style="display:none;">
                    <label>Select Month:</label>
                    <input type="month" id="selectedMonth" value="2026-10" onchange="updateMetrics()">
                </div>

                <div style="margin-left: auto; display: flex; gap: 8px;">
                    <button class="btn-main btn-success" onclick="downloadCSV('daily')">📥 Download Daily CSV</button>
                    <button class="btn-main" onclick="downloadCSV('monthly')">📊 Download Monthly CSV</button>
                </div>
            </div>

            <!-- Metrics Overview Cards -->
            <div class="metrics-grid">
                <div class="metric-card">
                    <h3>Total Enrolled</h3>
                    <p id="totalCount">0</p>
                </div>
                <div class="metric-card present">
                    <h3>Present</h3>
                    <p id="presentCount">0</p>
                </div>
                <div class="metric-card absent">
                    <h3>Absent</h3>
                    <p id="absentCount">0</p>
                </div>
                <div class="metric-card late">
                    <h3>Late / Excused</h3>
                    <p id="lateCount">0</p>
                </div>
                <div class="metric-card rate">
                    <h3>Attendance Rate</h3>
                    <p id="attendanceRate">0%</p>
                </div>
            </div>

            <!-- Charts Section -->
            <div class="charts-container">
                <!-- Visual Pie Chart with Percentages -->
                <div class="chart-box">
                    <h3>Attendance Distribution (Pie Chart with %)</h3>
                    <div class="pie-chart-wrapper">
                        <div class="pie-chart" id="statusPieChart">
                            <div class="pie-center-label">
                                <span class="center-pct" id="pieCenterRate">0%</span>
                                <span class="center-title">Rate</span>
                            </div>
                        </div>
                    </div>
                    <div class="chart-legend">
                        <div class="legend-row">
                            <div class="legend-item">
                                <div class="legend-dot" style="background:var(--success);"></div>
                                <span>Present</span>
                            </div>
                            <span class="pie-pct-badge" id="presentPctBadge" style="background:var(--success);">0%</span>
                        </div>
                        <div class="legend-row">
                            <div class="legend-item">
                                <div class="legend-dot" style="background:var(--danger);"></div>
                                <span>Absent</span>
                            </div>
                            <span class="pie-pct-badge" id="absentPctBadge" style="background:var(--danger);">0%</span>
                        </div>
                        <div class="legend-row">
                            <div class="legend-item">
                                <div class="legend-dot" style="background:var(--warning);"></div>
                                <span>Late / Excused</span>
                            </div>
                            <span class="pie-pct-badge" id="latePctBadge" style="background:var(--warning); color:#333;">0%</span>
                        </div>
                    </div>
                </div>

                <!-- Visual Bar Chart with Percentages -->
                <div class="chart-box">
                    <h3>Department-wise Attendance (%)</h3>
                    <div class="bar-chart" id="departmentBarChart">
                        <!-- Dynamic Bar items generated by JS -->
                    </div>
                </div>
            </div>

        </div>

        <!-- 2. ATTENDANCE ENTRY VIEW -->
        <div id="attendanceView" class="page-view">
            <div class="action-bar">
                <input type="text" class="search-box" id="searchBox" placeholder="Search by name, Reg No, or dept..." onkeyup="filterStudents()">
                <div>
                    <button class="btn-main" onclick="markAllPresent()">Mark All Present</button>
                    <button class="btn-main btn-success" onclick="downloadCSV('daily')">📥 Download CSV</button>
                </div>
            </div>

            <div class="table-responsive">
                <table>
                    <thead>
                        <tr>
                            <th>Reg No</th>
                            <th>Student Details</th>
                            <th>Department & Year</th>
                            <th>Student Mobile</th>
                            <th>Parent Mobile</th>
                            <th>Attendance Action</th>
                        </tr>
                    </thead>
                    <tbody id="studentTableBody">
                        <!-- Dynamic Rows populated by JS -->
                    </tbody>
                </table>
            </div>
        </div>

        <!-- 3. ADD STUDENT PAGE VIEW -->
        <div id="addStudentView" class="page-view">
            <h2 style="margin-bottom:10px; font-size:18px;">Add New Student Entry</h2>
            <p style="color:var(--text-muted); font-size:13px; margin-bottom:20px;">Enroll a new student into the active roster.</p>
            
            <form onsubmit="addNewStudent(event)">
                <div class="form-grid">
                    <div class="form-group">
                        <label>Register Number / Student ID *</label>
                        <input type="text" id="newRegNo" placeholder="e.g., 202605" required>
                    </div>

                    <div class="form-group">
                        <label>Full Name *</label>
                        <input type="text" id="newName" placeholder="e.g., Rahul Sharma" required>
                    </div>

                    <!-- Department Box with Manual Typing + Dropdown Arrow -->
                    <div class="form-group">
                        <label>Department Name (Type or Click Arrow) *</label>
                        <input type="text" id="newDept" list="departmentOptions" placeholder="Select or type department..." required>
                        <datalist id="departmentOptions">
                            <option value="Computer Science & Engineering (CSE)">
                            <option value="Information Technology (IT)">
                            <option value="Electronics & Communication (ECE)">
                            <option value="Electrical & Electronics (EEE)">
                            <option value="Mechanical Engineering (MECH)">
                            <option value="Civil Engineering (CIVIL)">
                            <option value="Artificial Intelligence & Data Science (AI & DS)">
                            <option value="Business Administration (MBA / BBA)">
                        </datalist>
                    </div>

                    <!-- Academic Year Dropdown -->
                    <div class="form-group">
                        <label>Academic Year *</label>
                        <select id="newYear" required>
                            <option value="">-- Select Year --</option>
                            <option value="1st Year">1st Year (1st / 2nd Sem)</option>
                            <option value="2nd Year">2nd Year (3rd / 4th Sem)</option>
                            <option value="3rd Year">3rd Year (5th / 6th Sem)</option>
                            <option value="4th Year">4th Year (7th / 8th Sem)</option>
                        </select>
                    </div>

                    <div class="form-group">
                        <label>Student Mobile Number *</label>
                        <input type="tel" id="newStudentMobile" placeholder="e.g., 9876543210" pattern="[0-9]{10}" required>
                    </div>

                    <div class="form-group">
                        <label>Email Address *</label>
                        <input type="email" id="newEmail" placeholder="e.g., student@college.edu" required>
                    </div>

                    <div class="form-group">
                        <label>Parent / Guardian Mobile Number *</label>
                        <input type="tel" id="newParentMobile" placeholder="e.g., 9876501234" pattern="[0-9]{10}" required>
                    </div>
                </div>

                <button type="submit" class="btn-main" style="margin-top: 15px;">Add Student to Roster</button>
            </form>
        </div>

    </div>

    <!-- JavaScript Application Logic -->
    <script>
        // Sample Roster Data
        let students = [
            { regNo: "202601", name: "Liam Johnson", dept: "Computer Science & Engineering (CSE)", year: "3rd Year", mobile: "9876543210", email: "liam@univ.edu", parentMobile: "9876501234", status: "Present" },
            { regNo: "202602", name: "Marcus Vance", dept: "Information Technology (IT)", year: "2nd Year", mobile: "9876543211", email: "marcus@univ.edu", parentMobile: "9876501235", status: "Absent" },
            { regNo: "202603", name: "Aaliyah Khan", dept: "Electronics & Communication (ECE)", year: "4th Year", mobile: "9876543212", email: "aaliyah@univ.edu", parentMobile: "9876501236", status: "Present" },
            { regNo: "202604", name: "Insans Flarmon", dept: "Computer Science & Engineering (CSE)", year: "3rd Year", mobile: "9876543213", email: "insans@univ.edu", parentMobile: "9876501237", status: "Late" }
        ];

        // Edit College Name Function
        function editCollegeName() {
            const currentName = document.getElementById('displayCollegeName').innerText.replace('🏛️ ', '');
            const newName = prompt("Enter your College Name:", currentName);
            if (newName && newName.trim() !== "") {
                document.getElementById('displayCollegeName').innerText = "🏛️ " + newName.trim();
            }
        }

        // Tab Switcher Function
        function switchTab(viewId, element) {
            document.querySelectorAll('.page-view').forEach(view => view.classList.remove('active'));
            document.querySelectorAll('.tab-btn').forEach(btn => btn.classList.remove('active'));
            
            document.getElementById(viewId).classList.add('active');
            element.classList.add('active');
        }

        // Handle Filter Toggle (Daily, Monthly, Yearly)
        function handleFilterChange() {
            const mode = document.getElementById('viewModeSelect').value;
            document.getElementById('datePickerGroup').style.display = (mode === 'daily') ? 'flex' : 'none';
            document.getElementById('monthPickerGroup').style.display = (mode === 'monthly') ? 'flex' : 'none';
            updateMetrics();
        }

        // Render Attendance Table
        function renderRoster() {
            const tbody = document.getElementById('studentTableBody');
            tbody.innerHTML = '';

            students.forEach((s, index) => {
                tbody.innerHTML += `
                    <tr>
                        <td><strong>${s.regNo}</strong></td>
                        <td><strong>${s.name}</strong><br><small style="color:#666;">${s.email}</small></td>
                        <td>${s.dept}<br><small style="color:#17a2b8; font-weight:600;">${s.year}</small></td>
                        <td>${s.mobile}</td>
                        <td>${s.parentMobile}</td>
                        <td>
                            <div class="status-btn-group">
                                <button class="status-btn present-btn ${s.status === 'Present' ? 'active' : ''}" onclick="setStatus(${index}, 'Present')">Present</button>
                                <button class="status-btn absent-btn ${s.status === 'Absent' ? 'active' : ''}" onclick="setStatus(${index}, 'Absent')">Absent</button>
                                <button class="status-btn late-btn ${s.status === 'Late' ? 'active' : ''}" onclick="setStatus(${index}, 'Late')">Late</button>
                                <button class="status-btn excused-btn ${s.status === 'Excused' ? 'active' : ''}" onclick="setStatus(${index}, 'Excused')">Excused</button>
                            </div>
                        </td>
                    </tr>
                `;
            });

            updateMetrics();
        }

        // Set Student Status
        function setStatus(index, status) {
            students[index].status = status;
            renderRoster();
        }

        // Mark All Present Action
        function markAllPresent() {
            students.forEach(s => s.status = 'Present');
            renderRoster();
        }

        // Add Student Form Handler
        function addNewStudent(e) {
            e.preventDefault();
            const regNo = document.getElementById('newRegNo').value;
            const name = document.getElementById('newName').value;
            const dept = document.getElementById('newDept').value;
            const year = document.getElementById('newYear').value;
            const mobile = document.getElementById('newStudentMobile').value;
            const email = document.getElementById('newEmail').value;
            const parentMobile = document.getElementById('newParentMobile').value;

            students.push({ regNo, name, dept, year, mobile, email, parentMobile, status: 'Present' });
            
            // Clear Form
            document.getElementById('newRegNo').value = '';
            document.getElementById('newName').value = '';
            document.getElementById('newDept').value = '';
            document.getElementById('newYear').value = '';
            document.getElementById('newStudentMobile').value = '';
            document.getElementById('newEmail').value = '';
            document.getElementById('newParentMobile').value = '';
            
            renderRoster();
            alert("New student enrolled successfully!");
            switchTab('attendanceView', document.querySelectorAll('.tab-btn')[1]);
        }

        // Real-time Metrics & Charts Calculation with Exact Pie & Bar % Badges
        function updateMetrics() {
            const total = students.length;
            const present = students.filter(s => s.status === 'Present').length;
            const absent = students.filter(s => s.status === 'Absent').length;
            const late = students.filter(s => s.status === 'Late' || s.status === 'Excused').length;
            
            const rate = total > 0 ? Math.round((present / total) * 100) : 0;
            const presentPct = total > 0 ? Math.round((present / total) * 100) : 0;
            const absentPct = total > 0 ? Math.round((absent / total) * 100) : 0;
            const latePct = total > 0 ? Math.round((late / total) * 100) : 0;

            document.getElementById('totalCount').innerText = total;
            document.getElementById('presentCount').innerText = present;
            document.getElementById('absentCount').innerText = absent;
            document.getElementById('lateCount').innerText = late;
            document.getElementById('attendanceRate').innerText = `${rate}%`;

            // Update Pie Chart Deg Angles & Percentage Badges
            document.getElementById('pieCenterRate').innerText = `${rate}%`;
            document.getElementById('presentPctBadge').innerText = `${presentPct}% (${present})`;
            document.getElementById('absentPctBadge').innerText = `${absentPct}% (${absent})`;
            document.getElementById('latePctBadge').innerText = `${latePct}% (${late})`;

            if (total > 0) {
                const presentDeg = presentPct;
                const absentDeg = presentPct + absentPct;

                document.getElementById('statusPieChart').style.setProperty('--present-deg', `${presentDeg}%`);
                document.getElementById('statusPieChart').style.setProperty('--absent-deg', `${absentDeg}%`);
            }

            // Update Department Bar Chart with Percentage Display
            const depts = {};
            students.forEach(s => {
                depts[s.dept] = (depts[s.dept] || 0) + (s.status === 'Present' ? 1 : 0);
            });

            const barContainer = document.getElementById('departmentBarChart');
            barContainer.innerHTML = '';
            
            for (let [deptName, count] of Object.entries(depts)) {
                const deptTotal = students.filter(s => s.dept === deptName).length;
                const deptRate = deptTotal > 0 ? Math.round((count / deptTotal) * 100) : 0;
                
                barContainer.innerHTML += `
                    <div class="bar-item">
                        <div class="bar-label">
                            <span>${deptName}</span>
                            <span class="pct-badge">${deptRate}% (${count}/${deptTotal} Present)</span>
                        </div>
                        <div class="bar-track">
                            <div class="bar-fill" style="width: ${deptRate}%"></div>
                        </div>
                    </div>
                `;
            }
        }

        // Search Filter
        function filterStudents() {
            const query = document.getElementById('searchBox').value.toLowerCase();
            const rows = document.querySelectorAll('#studentTableBody tr');
            rows.forEach(row => {
                const text = row.innerText.toLowerCase();
                row.style.display = text.includes(query) ? '' : 'none';
            });
        }

        // CSV Export Handler
        function downloadCSV(type) {
            let csv = "Register No,Student Name,Department,Year,Student Mobile,Email ID,Parent Mobile,Status\n";
            students.forEach(s => {
                csv += `"${s.regNo}","${s.name}","${s.dept}","${s.year}","${s.mobile}","${s.email}","${s.parentMobile}","${s.status}"\n`;
            });

            const blob = new Blob([csv], { type: 'text/csv' });
            const a = document.createElement('a');
            a.href = URL.createObjectURL(blob);
            a.download = `Attendance_${type}_Report.csv`;
            a.click();
        }

        // Initial Load
        renderRoster();
    </script>
</body>
</html>ck_canvas_web_portal.html…]()

