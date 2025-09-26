# DUTY-SIGN-IN-OUT

<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ระบบลงชื่อปฏิบัติหน้าที่ | สถานีดับเพลิง BIT Cities</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            color: #333;
            display: flex;
            justify-content: center;
            align-items: flex-start;
            min-height: 100vh;
            padding: 20px;
        }
        .container {
            background-color: #ffffff;
            padding: 40px;
            border-radius: 8px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
            width: 100%;
            max-width: 500px;
            text-align: center;
        }
        h1 {
            color: #cc0000;
            margin-bottom: 5px;
        }
        h2 {
            color: #555;
            margin-top: 0;
            font-weight: normal;
            font-size: 1.2em;
            margin-bottom: 25px;
        }
        .form-group {
            text-align: left;
            margin-bottom: 15px;
        }
        label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
        }
        input[type="text"],
        select#unitSelect {
            width: 95%;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 4px;
            font-size: 1em;
            box-sizing: border-box;
        }
        select#unitSelect {
            width: 100%;
            -webkit-appearance: none;
            -moz-appearance: none;
            appearance: none;
            background-color: white;
            background-image: url('data:image/svg+xml;charset=US-ASCII,%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20width%3D%22292.4%22%20height%3D%22292.4%22%3E%3Cpath%20fill%3D%22%23000000%22%20d%3D%22M287%2069.4a17.6%2017.6%200%200%200-13%205.1L146.2%20202.7%2018.8%2074.5a17.6%2017.6%200%200%200-25.3%200%2017.6%2017.6%200%200%200%200%2025.3l137%20137a17.6%2017.6%200%200%200%2025.3%200l137-137a17.6%2017.6%200%200%200%200-25.3%2017.6%2017.6%200%200%200-12.8-5.1z%22%2F%3E%3C%2Fsvg%3E');
            background-repeat: no-repeat;
            background-position: right 10px top 50%;
            background-size: 10px auto;
        }
        .button-group {
            display: flex;
            justify-content: space-between;
            gap: 10px;
            margin-top: 20px;
            margin-bottom: 30px;
        }
        .duty-button {
            flex-grow: 1;
            padding: 15px;
            border: none;
            border-radius: 6px;
            color: white;
            font-size: 1.1em;
            cursor: pointer;
            transition: background-color 0.3s;
            font-weight: bold;
        }
        .sign-in {
            background-color: #28a745;
        }
        .sign-in:hover {
            background-color: #218838;
        }
        .sign-out {
            background-color: #dc3545;
        }
        .sign-out:hover {
            background-color: #c82333;
        }
        .log-area {
            margin-top: 20px;
            padding: 15px;
            background-color: #eee;
            border-radius: 4px;
            text-align: left;
        }
        .log-area h3 {
            margin-top: 0;
            color: #333;
        }
        #dutyLog {
            list-style: none;
            padding: 0;
        }
        #dutyLog li {
            padding: 5px 0;
            border-bottom: 1px dotted #ccc;
            font-size: 0.9em;
        }
        #dutyLog li:last-child {
            border-bottom: none;
        }
        .status-message {
            margin-top: 10px;
            font-size: 1em;
            font-weight: bold;
        }
        .status-ok {
            color: #28a745;
        }
        .status-error {
            color: #dc3545;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>ระบบลงชื่อปฏิบัติหน้าที่</h1>
        <h2>สถานีดับเพลิงและกู้ภัย BIT Cities</h2>

        <div class="form-group">
            <label for="firefighterID">รหัสเจ้าหน้าที่:</label>
            <input type="text" id="firefighterID" name="firefighterID" placeholder="ป้อนรหัส เช่น FR-001" required>
        </div>

        <div class="form-group">
            <label for="unitSelect">เลือกหน่วยปฏิบัติหน้าที่:</label>
            <select id="unitSelect" name="unitSelect" required>
                <option value="" disabled selected>-- กรุณาเลือกหน่วย --</option>
                <option value="SAWANG ZITE BIT (EMT)">SAWANG ZITE BIT (EMT)</option>
                <option value="ATV LANCE (ATL)">ATV LANCE (ATL)</option>
                <option value="ปภ. (DDPM)">ปภ. (DDPM)</option>
                <option value="ดับเพลิง/กู้ภัยดับเพลิง (BFRD)">ดับเพลิง/กู้ภัยดับเพลิง (BFRD)</option>
            </select>
        </div>

        <div class="button-group">
            <button class="duty-button sign-in" onclick="logAction('ขึ้นเวร')">ขึ้นเวร (Sign In)</button>
            <button class="duty-button sign-out" onclick="logAction('ลงเวร')">ลงเวร (Sign Out)</button>
        </div>
        
        <div class="log-area">
            <h3>บันทึกการปฏิบัติหน้าที่ล่าสุด</h3>
            <ul id="dutyLog">
                <li>[19:00:00] BFRD | รหัส FR-001: ลงเวรสำเร็จ</li>
                <li>[07:00:00] SAWANG ZITE BIT (EMT) | รหัส EMT-025: ขึ้นเวรสำเร็จ</li>
            </ul>
        </div>
    </div>
    <script>
        // ใช้ JavaScript Map เพื่อเก็บสถานะของเจ้าหน้าที่แต่ละคน
        // key: รหัสเจ้าหน้าที่, value: true (ขึ้นเวรแล้ว) หรือ false (ลงเวรแล้ว)
        const dutyStatus = new Map();

        function logAction(actionType) {
            const id = document.getElementById('firefighterID').value.toUpperCase().trim();
            const unit = document.getElementById('unitSelect').value;
            const logList = document.getElementById('dutyLog');

            if (!unit) {
                alert('กรุณาเลือกหน่วยปฏิบัติหน้าที่!');
                return;
            }

            const idPattern = /^[A-Z]{2,3}-\d{2,3}$/;
            if (!idPattern.test(id)) {
                alert('รหัสเจ้าหน้าที่ไม่ถูกต้อง! รหัสต้องเป็น ENG 2-3 ตัว - เลข 2-3 หลัก (เช่น FR-12, EMT-050)');
                return;
            }

            const isCurrentlyOnDuty = dutyStatus.get(id) || false;

            if (actionType === 'ขึ้นเวร') {
                if (isCurrentlyOnDuty) {
                    alert('ไม่สามารถขึ้นเวรซ้ำได้! เจ้าหน้าที่คนนี้ยังอยู่ในสถานะ "ขึ้นเวร"');
                    return;
                }
                dutyStatus.set(id, true); // ตั้งค่าสถานะเป็น "ขึ้นเวรแล้ว"
            } else if (actionType === 'ลงเวร') {
                if (!isCurrentlyOnDuty) {
                    alert('ไม่สามารถลงเวรได้! เจ้าหน้าที่คนนี้ยังไม่ได้อยู่ในสถานะ "ขึ้นเวร"');
                    return;
                }
                dutyStatus.set(id, false); // ตั้งค่าสถานะเป็น "ลงเวรแล้ว"
            }

            const now = new Date();
            const timeString = now.toLocaleTimeString('th-TH', { hour: '2-digit', minute: '2-digit', second: '2-digit' });
            const newLogItem = document.createElement('li');

            if (actionType === 'ขึ้นเวร') {
                newLogItem.innerHTML = `[${timeString}] **${unit}** | รหัส **${id}**: <b>ขึ้นเวรสำเร็จ</b>`;
                newLogItem.style.color = '#28a745';
            } else {
                newLogItem.innerHTML = `[${timeString}] **${unit}** | รหัส **${id}**: <b>ลงเวรสำเร็จ</b>`;
                newLogItem.style.color = '#dc3545';
            }

            logList.prepend(newLogItem);
            document.getElementById('firefighterID').value = '';
        }
    </script>
</body>
</html>
