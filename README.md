# Shalehna

**Course:** Electronic Business Development (BINF 503) · Winter 2026
**Instructor:** Dr. Nourhan Hamdi
**Teaching Assistant:** Mr. Nour Gaser

## 1. Team

| Name | Student ID | Tutorial group | GitHub username |
|---|---|---|---|
| Karim Tamer Anan | 14003334 | T6 | tamer77anan-del |
| Youssef Rawy | 13006981 | T6 | yousseffrrawyy |

## 2. The idea

Shalehna is a web app for Egyptian families and friends who share one chalet in Sahel or Sokhna. Today they run the summer from a WhatsApp group and a notebook: who takes which week, who paid the maintenance fee, and what happens to the weeks nobody uses. In Shalehna, the co-owners book weeks for their own families, rent the free weeks to guests with an owner's approval, and log the shared expenses. Their dashboard shows the chalet's income and costs, and each owner's share of them.

## 3. Features

### 3.1 The full product

- Register and log in as a chalet owner or a guest
- Create a chalet with its area, price per week and number of summer weeks
- Add co-owners to a chalet, each with their share
- Book a summer week for your own family
- Guests request free weeks, and owners accept or reject them
- Log shared expenses such as maintenance, utilities, compound fees and fines, and real-estate tax
- A dashboard with rental income, expenses, net profit, how the weeks are used and each owner's share
- Share the free weeks on WhatsApp
- Add a booked week to Google Calendar
- See the chalet's location on a map
- See the weather forecast for the chalet's area

### 3.2 The use cases we will build

| # | Use case | What the user does | What they see | What is stored |
|---|---|---|---|---|
| 1 | Registration and login | Registers with name, email, password and role (owner or guest); logs in with email and password | Their home page, with their name in the header | A User, with the password hashed |
| 2 | Manage a chalet | An owner creates a chalet with its name, area, price per week and number of summer weeks, edits it, adds or removes a co-owner by email with their share, or deletes it | The list of their chalets, each with its owners and their shares | A Chalet, with its owners and their shares |
| 3 | Family week booking | An owner books a free week for their family or cancels it; a week that is already taken cannot be booked | The chalet's summer weeks, each one free or booked by a family | A Booking of type family, with its chalet, owner and week number |
| 4 | Guest rental | A guest requests a free week or cancels the request; an owner accepts or rejects it | The guest sees their requests and their status; the owner sees the requests for their chalet | A Booking of type rental, with its chalet, guest, week number and status |
| 5 | Expenses and dashboard | An owner logs a shared expense with its title, type and amount, edits it, or deletes it | The list of expenses and a dashboard: rental income, total expenses, net profit, weeks by status, and each owner's share | An Expense, linked to its chalet |

## 4. Who owns what

| Member | Use case |
|---|---|
| Karim Tamer Anan | 1. Registration and login |
| Youssef Rawy | 2. Manage a chalet |
| Karim Tamer Anan | 3. Family week booking |
| Youssef Rawy | 4. Guest rental |
| Karim Tamer Anan | 5. Expenses and dashboard |

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
  area: { type: String, required: true },
  pricePerWeek: { type: Number, required: true },
  weeks: { type: Number, required: true },
  owners: [
    {
      user: { type: mongoose.Schema.Types.ObjectId, ref: "User" },
      share: { type: Number, required: true },
    },
  ],
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
