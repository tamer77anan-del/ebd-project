# Shalehna

**Course:** Electronic Business Development (BINF 503) · Winter 2026
**Instructor:** Dr. Nourhan Hamdi
**Teaching Assistants:** Mr. Nour Gaser, Mr. Omar Alaa, Ms. Mariam Khalid, Mr. Younes Zied, Mr. Mahmoud Hani

## 1. Team

| Name | Student ID | Tutorial group | GitHub username |
|---|---|---|---|
| Karim Tamer Anan | 14003334 | T6 | tamer77anan-del |
| Youssef Rawy | 13006981 | T6 | yousseffrrawyy |

## 2. The idea

Shalehna is a web app for Egyptian families and friends who share one chalet in Sahel or Sokhna. Today they run the summer from a WhatsApp group and a notebook: who takes which week, who paid the maintenance fee, and what happens to the weeks nobody uses. In Shalehna, the owners book weeks for their own families, rent the free weeks to guests and log the shared expenses. Their dashboard shows what the chalet earns and what it costs.

## 3. Features

### 3.1 The full product

- Register and log in as a chalet owner or a guest
- Create a chalet with its location, price per week and number of summer weeks
- Book a summer week for your own family
- Guests request free weeks, and owners accept or reject them
- Log shared expenses such as maintenance, electricity and cleaning
- A dashboard with rental income, expenses, net profit and how the weeks are used

### 3.2 The use cases we will build

| # | Use case | What the user does | What they see | What is stored |
|---|---|---|---|---|
| 1 | Registration and login | Registers with name, email, password and role (owner or guest); logs in with email and password | Their home page, with their name in the header | A User, with the password hashed |
| 2 | Manage a chalet | An owner creates a chalet with its name, location, price per week and number of summer weeks, edits it, or deletes it | The list of their chalets with each chalet's details | A Chalet, linked to its owner |
| 3 | Book a week | An owner books a free week for their family; a guest requests a free week; an owner accepts or rejects a guest's request; either one cancels a booking | The chalet's summer weeks, each one marked free, family, requested or rented | A Booking, with its chalet, user, week number, type and status |
| 4 | Expenses and dashboard | An owner logs a shared expense with its title, type and amount, or deletes a wrong one | The list of expenses and a dashboard: rental income, total expenses, net profit, and weeks by status | An Expense, linked to its chalet |

## 4. Who owns what

## 5. Data model

### User

```js
const userSchema = new mongoose.Schema({
  name: { type: String, required: true },
  email: { type: String, required: true, unique: true },
  password: { type: String, required: true }, // stored hashed, never as plain text
  role: { type: String, required: true },
});
```

### Chalet

```js
const chaletSchema = new mongoose.Schema({
  name: { type: String, required: true },
  location: { type: String, required: true },
  pricePerWeek: { type: Number, required: true },
  weeks: { type: Number, required: true },
  owner: { type: mongoose.Schema.Types.ObjectId, ref: "User", required: true },
});
```

### Booking

```js
const bookingSchema = new mongoose.Schema({
  chalet: { type: mongoose.Schema.Types.ObjectId, ref: "Chalet", required: true },
  user: { type: mongoose.Schema.Types.ObjectId, ref: "User", required: true },
  week: { type: Number, required: true },
  type: { type: String, required: true },
  status: { type: String, default: "pending" },
});
```

### Expense

```js
const expenseSchema = new mongoose.Schema({
  chalet: { type: mongoose.Schema.Types.ObjectId, ref: "Chalet", required: true },
  title: { type: String, required: true },
  type: { type: String, required: true },
  amount: { type: Number, required: true },
});
```

## 6. Run it locally

> Leave this section as it is until Submission 2 (Thursday 10 December 2026,
> 23:59). Then fill it in: we follow these steps to run your project.

### Back end

```bash
cd backend
npm install
# create backend/.env from backend/.env.example (see the table below)
npm start
```

The API runs on http://localhost:3000.

| Variable in `.env` | What it is |
|---|---|
| `MONGODB_URI` | The connection string of your MongoDB Atlas database |
| `JWT_SECRET` | Any long random text, used to sign login tokens |
| [Any other variable] | [What it is] |

### Front end

```bash
cd frontend
npm install
npm run dev
```

The app runs on [the address `npm run dev` prints, e.g. http://localhost:5173].
