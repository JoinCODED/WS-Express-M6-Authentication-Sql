We will add the functionality for the `student` to sign up and signin.

Fork and clone [this](https://github.com/JoinCODED/Demo-Express-M6-Authentication-Sql/) into your development folder.

1. Modify the `student` model, add a field for the password.

```js
const StudentModel = (sequelize, DataTypes) => {
  const Student = sequelize.define('Student', {
    name: {
      type: DataTypes.STRING,
    },
    password: {
      type: DataTypes.STRING,
      allowNull: false,
    },
  });
  return Student;
};

module.exports = StudentModel;
```

2. Let's modify our `student` create route:

```js
router.post('/signup', studentsCreate);
```

3. And rename `studentsCreate` to `signup`.

```js
router.post('/signup', signup);
```

```js
exports.signup = async (req, res) => {
  try {
    const newStudent = await Student.create(req.body);
    res.status(201).json(newStudent);
  } catch (error) {
    res.status(500).json({ message: error.message });
  }
};
```

4. Let's test it with Postman. Voila! It worked! But something looks wrong. As a user, how comfortable do you feel knowing that your password can be easily accessed by anyone who has access to the database? We need some kind of method to encrypt our password.
