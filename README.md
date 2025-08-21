# library-api
README.mdconst express = require("express");
const app = express();
app.use(express.json());

let books = [
  { id: 1, title: "IoT Basics", author: "John Doe" },
  { id: 2, title: "Digital Electronics", author: "Smith" }
];

// Get all books
app.get("/books", (req, res) => res.json(books));

// Add a new book
app.post("/books", (req, res) => {
  const newBook = { id: books.length + 1, ...req.body };
  books.push(newBook);
  res.json(newBook);
});

// Update a book
app.put("/books/:id", (req, res) => {
  const book = books.find(b => b.id == req.params.id);
  if (!book) return res.status(404).send("Book not found");
  Object.assign(book, req.body);
  res.json(book);
});

// Delete a book
app.delete("/books/:id", (req, res) => {
  books = books.filter(b => b.id != req.params.id);
  res.send("Book deleted");
});

app.listen(3000, () => console.log("📚 API running at http://localhost:3000"));
