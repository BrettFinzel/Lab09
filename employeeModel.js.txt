const mongoose = require('mongoose');

const employeeSchema = new mongoose.Schema({
  name: String,
  age: Number,
  country: String,
  position: String,
  wage: Number,
});

const Employee = mongoose.model('Employee', employeeSchema);

module.exports = Employee;
