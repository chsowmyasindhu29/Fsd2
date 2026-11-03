 npm init 
npm install express
Step 2: Create server.js

const express = require('express');

const app = express();
const PORT = 3000;

app.use(express.json());

// Custom middleware
app.use((req, res, next) => {
    console.log("Method:", req.method);
    console.log("URL:", req.originalUrl);
    next();
});

app.get('/', (req, res) => {
    res.send("Welcome to ExpressJS!");
});

app.get('/user/:id', (req, res) => {
    res.send("User ID: " + req.params.id);
});

app.get('/search', (req, res) => {
    const q = req.query.q;
    const limit = req.query.limit;

    res.send(`Search: ${q}, Limit: ${limit}`);
});

app.get('/students', (req, res) => {
    res.json(["Ravi", "Sita", "Kiran"]);
});

app.post('/students', (req, res) => {
    res.json({
        message: "Student added successfully",
        student: req.body
    });
});

app.delete('/students/:id', (req, res) => {
    res.send("Student with ID " + req.params.id + " deleted");
});

app.listen(PORT, () => {
    console.log(`Server running at http://localhost:${PORT}`);
});
