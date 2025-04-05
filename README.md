<!DOCTYPE html>
<html>
<head>
    <title>学生成绩管理系统</title>
    <style>
        .red-name { color: red; }
        table { border-collapse: collapse; margin: 20px; }
        td, th { border: 1px solid #999; padding: 8px 15px; }
        button { margin-left: 20px; padding: 5px 15px; }
    </style>
</head>
<body>
    <table>
        <thead>
            <tr>
                <th>姓名</th>
                <th>学号</th>
                <th>得分</th>
            </tr>
        </thead>
        <tbody id="dataContainer"></tbody>
    </table>
    <button onclick="addStudent()">添加学生</button>

    <script>
        // 姓氏库（包含单姓和复姓）
        const surnames = [
            '王','李','张','刘','陈','杨','黄','赵','周','吴',
            '欧阳','司马','上官','诸葛','令狐','宇文','慕容','公孙','轩辕','皇甫'
        ];

        // 名字库
        const givenNames = [
            '伟','芳','强','丽','娜','敏','静','杰','涛','明',
            '婷婷','子轩','雨欣','浩然','欣怡','博文','诗涵','俊杰','雅雯','宇航',
            '若曦','天佑','梦瑶','晨曦','梓萱','睿渊','美琳','浩宇','思彤','泽洋'
        ];

        // 生成随机姓名函数
        function generateName() {
            const surname = surnames[Math.floor(Math.random() * surnames.length)];
            const givenName = givenNames[Math.floor(Math.random() * givenNames.length)];
            
            // 30%概率给双字名（如果名字库包含双字选项）
            return Math.random() < 0.3 && givenName.length === 2 
                   ? `${surname}${givenName}`
                   : `${surname}${givenNames[Math.floor(Math.random() * 10)]}`;  // 前10个是单字
        }

        // 初始化学生数据
        let students = Array.from({length:4}, () => ({
            name: generateName(),
            number: 'S2023' + Math.floor(1000 + Math.random() * 9000),
            score: Math.floor(Math.random() * 100)
        }));

        // 表格渲染函数
        function renderTable() {
            const tbody = document.getElementById('dataContainer');
            tbody.innerHTML = '';

            students.forEach(student => {
                const tr = document.createElement('tr');
                
                // 姓名列（带样式判断）
                const nameTd = document.createElement('td');
                nameTd.textContent = student.name;
                if(student.score < 60) nameTd.classList.add('red-name');
                
                // 学号列
                const numTd = document.createElement('td');
                numTd.textContent = student.number;
                
                // 分数列
                const scoreTd = document.createElement('td');
                scoreTd.textContent = student.score;

                tr.append(nameTd, numTd, scoreTd);
                tbody.appendChild(tr);
            });
        }

        // 添加新学生
        function addStudent() {
            students.push({
                name: generateName(),
                number: 'S2023' + Math.floor(1000 + Math.random() * 9000),
                score: Math.floor(Math.random() * 100)
            });
            renderTable();
        }

        // 初始渲染
        renderTable();
    </script>
</body>
</html>
