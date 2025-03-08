<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Digital Bookshelf</title>
    <style>
        /* ... (Your existing styles) ... */
        #urlForm {
            margin-top: 20px;
            text-align: center;
        }
    </style>
    <link href="https://fonts.googleapis.com/css2?family=Dancing+Script&display=swap" rel="stylesheet">
</head>
<body>
    <h1>My Digital Bookshelf</h1>
    <div id="bookshelf"></div>
    <div id="urlForm">
        <input type="text" id="pdfUrl" placeholder="PDF URL">
        <input type="text" id="imageUrl" placeholder="Image URL">
        <input type="text" id="bookTitle" placeholder="Book Title">
        <button onclick="addBookFromUrl()">Add Book</button>
    </div>
    <script>
        let books = JSON.parse(localStorage.getItem("books")) || [];

        function saveBooks() {
            try {
                localStorage.setItem("books", JSON.stringify(books));
                console.log("Books saved successfully:", JSON.parse(localStorage.getItem("books")));
            } catch (e) {
                if (e instanceof DOMException && e.code === 22) {
                    alert("Local storage is full. Please remove some books.");
                } else {
                    console.error("Error saving books:", e, books);
                    alert("An error occurred while saving books.");
                }
            }
        }

        function displayBooks() {
            const bookshelf = document.getElementById("bookshelf");
            bookshelf.innerHTML = "";
            books.forEach(book => {
                const bookDiv = document.createElement("div");
                bookDiv.classList.add("book");
                const bookLink = document.createElement("a");
                bookLink.href = book.pdfUrl; // Use pdfUrl
                bookLink.download = book.title + ".pdf";
                const coverImg = document.createElement("img");
                coverImg.src = book.imageUrl; // Use imageUrl
                coverImg.alt = book.title + " Cover";
                coverImg.onerror = function() {
                    console.error("Image load error for:", book.title);
                };
                const titlePara = document.createElement("p");
                titlePara.textContent = book.title;
                bookLink.appendChild(coverImg);
                bookLink.appendChild(titlePara);
                bookDiv.appendChild(bookLink);
                bookshelf.appendChild(bookDiv);
            });
        }

        displayBooks();

        function addBookFromUrl() {
            const pdfUrl = document.getElementById("pdfUrl").value;
            const imageUrl = document.getElementById("imageUrl").value;
            const bookTitle = document.getElementById("bookTitle").value;

            if (pdfUrl && imageUrl && bookTitle) {
                const newBook = {
                    title: bookTitle,
                    imageUrl: imageUrl,
                    pdfUrl: pdfUrl,
                };
                books.push(newBook);
                saveBooks();
                displayBooks();
                document.getElementById("pdfUrl").value = "";
                document.getElementById("imageUrl").value = "";
                document.getElementById("bookTitle").value = "";
            } else {
                alert("Please enter all URLs and the book title.");
            }
        }
    </script>
</body>
</html>
