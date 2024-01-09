# VueMyNotes: Vue.js Note-Taking App

## Introduction
VueMyNotes is a dynamic, single-page note-taking app built with Vue.js. This project showcases my skills in front-end development and my ability to create user-friendly web applications.

## Setup
Clone the repository and install dependencies:
```bash
git clone https://github.com/paolacernada/VueMyNotes.git
cd MyVueNotes
npm install
```

Start the application:
```bash
npm start
```
Access the app at `http://localhost:5173` and the API at `http://localhost:3000/notes/`.

## Features
- Add, view, edit, and delete notes.
- Real-time updates without page refreshes.
- User-friendly interface with Vue.js and Tailwind CSS.
- Integrated with Vue DevTools.

## API Usage
Example of adding a new note:
```javascript
fetch('http://localhost:3000/notes/', {
  method: 'POST',
  headers: {"Content-Type": "application/json"},
  body: JSON.stringify({ title, body, updatedAt: new Date() })
})
.then(response => response.json())
.then(data => console.log(data))
```

## Why VueMyNotes?
VueMyNotes reflects my Vue.js capabilities and my passion for creating engaging web applications. It's designed to be a practical tool for users and a showcase of my coding journey.
