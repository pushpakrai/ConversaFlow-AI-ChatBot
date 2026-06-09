
🤖 ConversaFlow AI

---
**A modern, AI-powered chatbot built with the MERN stack, designed for seamless integration and intelligent conversations.**

ChatBot-AI is a **scalable, beginner-friendly**, and **production-ready** application that enables **real-time, context-aware conversations** with users. It features a **floating chat widget**, **visitor onboarding**, **admin analytics**, and **Groq API integration** for ultra-fast AI responses. Built with **simplicity and performance** in mind, it uses **React.js, Node.js, Express.js, and MongoDB** to deliver a robust and responsive experience.

---

## 🌟 **Why ChatBot-AI?**
✅ **Easy Integration**: Embed the chatbot widget with a **single line of code**.
✅ **Personalized Interactions**: Collect visitor details (Name, Profession, Goal) to **tailor AI responses**.
✅ **Admin Dashboard**: Monitor **metrics, visitor counts, and chat transcripts** in a clean, read-only portal.
✅ **Responsive Design**: Works **flawlessly on desktop and mobile** devices.
✅ **Production-Ready**: Deploy with confidence using **Render, Heroku, AWS, or any cloud provider**.
✅ **Beginner-Friendly**: Clean, **well-documented code** with **no overengineering**.

---

## ✨ **Key Features**

### 🔌 **Floating Chatbot Widget**
- Embeddable via a **single `<script>` tag**.
- Appears at the **bottom-right** of any webpage.
- **Customizable** size, color, and behavior.

### 🧑‍💻 **Visitor Onboarding**
- Collects **Name, Profession, and Goal** on first interaction.
- Uses this data to **personalize AI responses** dynamically.

### 🧠 **Smart Context System**
- Prefixes user inputs with **visitor details** for **context-aware conversations**.
- Powered by the **Groq API** for **ultra-fast LLM responses**.

### 📊 **Admin Dashboard**
- **Read-only portal** for viewing:
  - Total visitors, conversations, and messages.
  - **Searchable chat transcripts**.
  - **Profession breakdown** of visitors.

### 🔒 **Password Protection**
- Simple `window.prompt` password gate for `/admin` access.
- Default password: `varta123` (customizable in `.env`).

### 🎨 **Responsive UI**
- Built with **Bootstrap 5** for a **sleek, fast, and mobile-friendly** experience.
- **Desktop**: 400px × 600px popup with rounded corners.
- **Mobile**: Scales to **100% width/height** for screens < 480px.

### ☁️ **Production-Ready Deployment**
- Compiles **React frontend** into the **Express backend** for single-port deployment.
- Compatible with **Render, Heroku, AWS, and other cloud providers**.

---

## 📁 **Project Structure**

```text
ChatBot-AI/
├── frontend/                     # React SPA (Vite, Bootstrap, Custom Router)
│   ├── src/
│   │   ├── components/
│   │   │   ├── AdminDashboard.jsx # Admin stats & chat viewer
│   │   │   ├── WidgetChat.jsx     # Onboarding form & Chat UI
│   │   │   └── ChatWindow.jsx     # Main chat interface
│   │   ├── App.jsx                # Custom routing layer
│   │   ├── index.css              # Custom CSS overrides
│   │   └── main.jsx
│   └── index.html
├── server/                       # Express API Backend & MongoDB Schemas
│   ├── models/                   # Mongoose schemas
│   │   ├── Visitor.js
│   │   ├── Conversation.js
│   │   └── Message.js
│   ├── public/                   # Static assets
│   │   └── widget.js             # Loader script for client websites
│   ├── config/                   # Configuration files
│   │   └── env.js                # Environment variables
│   ├── routes/                   # API routes
│   │   ├── widgetRoutes.js       # Widget-related endpoints
│   │   └── adminRoutes.js        # Admin dashboard endpoints
│   └── server.js                 # Main server router & DB connector
├── index.html                    # Demo website embedding the widget
└── package.json                  # Root orchestration runner
```

---

## 🚀 **Quick Start Guide**

### **Prerequisites**
- **Node.js** (v16+)
- **MongoDB** (local or Atlas URI)
- **Groq API Key** ([Get one here](https://console.groq.com/))

---

### **1. Clone the Repository**
```bash
git clone https://github.com/pushpakrai/ChatBot-AI-.git
cd ChatBot-AI-
```

---

### **2. Configure Environment Variables**
Navigate to the `server/` directory, copy `.env.example` to `.env`, and update the following:
```bash
PORT=5000
MONGO_URI=mongodb://127.0.0.1:27017/chatbot_ai
GROQ_API_KEY=your_groq_api_key_here
ADMIN_PASSWORD=your_custom_password
```

---
### **3. Install Dependencies**
Run the following command in the **root folder** to install dependencies for all directories:
```bash
npm run install-all
```

---
### **4. Start Development Servers**
```bash
npm run dev
```
- **Frontend Dev Hub**: [http://localhost:5173](http://localhost:5173)
- **Admin Portal**: [http://localhost:5173/admin](http://localhost:5173/admin)
- **Express API Server**: [http://localhost:5000](http://localhost:5000)

---
### **5. Test the Widget**
Open the root `index.html` file in any browser. The **floating chat button** will appear at the bottom-right corner!

---

## 🔌 **Widget Embed Guide**

### **How to Embed on Any Website**
Insert the following script tag **anywhere inside the `<body>`** of your HTML files:
```html
<script src="http://localhost:5000/widget.js"></script>
```
**Note**: Replace `http://localhost:5000` with your **production backend server domain** once deployed.

---
### **Sizing and Responsiveness**
| Device       | Dimensions               | Behavior                          |
|--------------|--------------------------|-----------------------------------|
| **Desktop**  | 400px × 600px            | Popup window with rounded corners |
| **Mobile**   | 100% width/height        | Full-screen chat interface        |

---

## 📡 **API Endpoint Reference**

All JSON payloads are sent using the `Content-Type: application/json` header.

---
### **1. Onboard Visitor**
**Endpoint**: `POST /api/widget/onboard`
**Description**: Creates a new visitor profile and initializes an active conversation session.

**Request Body**:
```json
{
  "name": "Jane Doe",
  "profession": "Founder",
  "goal": "Pricing check"
}
```

**Response (201 Created)**:
```json
{
  "visitorId": "65f3a09e...",
  "conversationId": "65f3a09f...",
  "visitorName": "Jane Doe"
}
```

---
### **2. Fetch History**
**Endpoint**: `GET /api/widget/history/:visitorId`
**Description**: Retrieves previous conversations and message logs to resume a session.

**Response (200 OK)**:
```json
{
  "visitorName": "Jane Doe",
  "conversationId": "65f3a09f...",
  "messages": [
    { "sender": "ai", "text": "Hi Jane! How can I help you?", "createdAt": "2026-06-07T10:00:00Z" }
  ]
}
```

---
### **3. Send Message**
**Endpoint**: `POST /api/widget/chat`
**Description**: Submits a message to the assistant. The backend automatically prefixes the system instructions with the visitor's profile details.

**Request Body**:
```json
{
  "visitorId": "65f3a09e...",
  "conversationId": "65f3a09f...",
  "text": "Tell me about your pricing."
}
```

**Response (200 OK)**:
```json
{
  "reply": "Hi Jane! Our pricing starts at $10/month. Would you like a detailed breakdown?"
}
```

---
### **4. Admin Analytics**
**Endpoint**: `GET /api/analytics`
**Description**: Aggregates statistical totals for display on the Admin dashboard.

**Response (200 OK)**:
```json
{
  "totalVisitors": 12,
  "totalConversations": 14,
  "totalMessages": 82,
  "professionBreakdown": [
    { "_id": "Founder", "count": 6 },
    { "_id": "Developer", "count": 4 }
  ]
}
```

---
### **5. Search Conversations**
**Endpoint**: `GET /api/admin/search?q=query`
**Description**: Search for conversations by visitor name, profession, or goal.

**Response (200 OK)**:
```json
{
  "results": [
    {
      "visitorId": "65f3a09e...",
      "visitorName": "Jane Doe",
      "profession": "Founder",
      "goal": "Pricing check",
      "messages": [...]
    }
  ]
}
```
---
## 🛠️ **Tech Stack**

| Category       | Technologies          |
|----------------|-----------------------|
| **Frontend**   | React.js, Vite, Bootstrap 5 |
| **Backend**    | Node.js, Express.js   |
| **Database**   | MongoDB, Mongoose     |
| **AI**         | Groq API              |
| **Styling**    | Custom CSS, Bootstrap |
| **Deployment** | Render, Heroku, AWS   |

---
## 💡 **Tips & Best Practices**
- **Security**: Always **customize** the `ADMIN_PASSWORD` in `.env` for production.
- **Performance**: Use **Groq API** for **ultra-fast LLM responses**.
- **Scalability**: Deploy on **Render, Heroku, or AWS** for seamless scaling.
- **Customization**: Modify the **Bootstrap theme** or **CSS** to match your brand.
- **Monitoring**: Use tools like **PM2** or **Docker** for process management.

---
## 📜 **License**
This project is **open-source** and available under the **[MIT License](LICENSE)**.

---
## 🤝 **Contributing**
Contributions are **welcome**! Please:
1. Fork the repository.
2. Create a **feature branch** (`git checkout -b feature/your-feature`).
3. Commit your changes (`git commit -m "Add your feature"`).
4. Push to the branch (`git push origin feature/your-feature`).
5. Open a **Pull Request**.

---
## 📧 **Support**
For issues or questions:
- Open an **issue** on [GitHub](https://github.com/pushpakrai/ChatBot-AI-/issues).
- Contact the maintainers at **pushpakrai@example.com**.

---
## 📚 **Additional Resources**
- [Groq API Documentation](https://console.groq.com/docs)
- [MongoDB Atlas Setup](https://www.mongodb.com/atlas/database)
- [React.js Documentation](https://react.dev/)
- [Express.js Documentation](https://expressjs.com/)
