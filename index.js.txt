const express = require('express');
const mongoose = require('mongoose');
const bodyParser = require('body-parser');
const app = express();
const PORT = process.env.PORT || 3000;

// Connect to MongoDB (replace 'your_database_url' with your actual database URL)
mongoose.connect('your_database_url', { useNewUrlParser: true, useUnifiedTopology: true });

// Create a Mongoose schema for the employee model
const employeeSchema = new mongoose.Schema({
  name: String,
  age: Number,
  country: String,
  position: String,
  wage: Number,
});

const Employee = mongoose.model('Employee', employeeSchema);

// Middleware to parse incoming JSON requests
app.use(bodyParser.json());

// Route to add an employee
app.post('/addEmployee', async (req, res) => {
  try {
    const newEmployee = new Employee(req.body);
    await newEmployee.save();
    res.status(201).send('Employee added successfully.');
  } catch (error) {
    res.status(500).send(error.message);
  }
});

// Route to get all employees
app.get('/getEmployees', async (req, res) => {
  try {
    const employees = await Employee.find();
    res.status(200).json(employees);
  } catch (error) {
    res.status(500).send(error.message);
  }
});

app.listen(PORT, () => {
  console.log(`Server is running on http://localhost:${PORT}`);
});
