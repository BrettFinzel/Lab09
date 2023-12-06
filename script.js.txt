async function addEmployee() {
  const name = document.getElementById('name').value;
  const age = parseInt(document.getElementById('age').value);
  const country = document.getElementById('country').value;
  const position = document.getElementById('position').value;
  const wage = parseInt(document.getElementById('wage').value);

  try {
    const response = await fetch('/addEmployee', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify({ name, age, country, position, wage }),
    });

    if (response.ok) {
      alert('Employee added successfully.');
    } else {
      alert('Error adding employee. Please try again.');
    }
  } catch (error) {
    console.error('Error:', error);
  }
}

async function showEmployees() {
  try {
    const response = await fetch('/getEmployees');
    const employees = await response.json();

    const employeeList = document.getElementById('employeeList');
    employeeList.innerHTML = '';

    employees.forEach((employee) => {
      const employeeInfo = document.createElement('div');
      employeeInfo.innerHTML = `
        <strong>Name:</strong> ${employee.name}<br>
        <strong>Age:</strong> ${employee.age}<br>
        <strong>Country:</strong> ${employee.country}<br>
        <strong>Position:</strong> ${employee.position}<br>
        <strong>Wage:</strong> ${employee.wage}<br><br>
      `;
      employeeList.appendChild(employeeInfo);
    });
  } catch (error) {
    console.error('Error:', error);
  }
}
