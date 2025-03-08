<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Digital Bookshelf</title>
    <style>
        body {
            font-family: 'Brush Script MT', 'Brush Script Std', cursive;
            font-size: 10px;
            margin: 20px;
            background-color: #ddc6c6;
        }
        h1 {
            text-align: center;
        }
        #bookshelf {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
            gap: 20px;
            padding: 20px;
        }
        .book {
            text-align: center;
            background-color: #fff;
            border: 1px solid #ddd;
            padding: 10px;
            box-shadow: 2px 2px 5px rgba(0, 0, 0, 0.1);
        }
        .book img {
            max-width: 100%;
            height: auto;
            display: block;
            margin-bottom: 10px;
        }
        .book a {
            text-decoration: none;
            color: #333;
        }
        .book a:hover {
            color: #007bff;
        }
        .book p {
            font-size: 12px;
            margin-top: 5px;
            margin-bottom: 0;
            line-height: 1.2;
            overflow: hidden;
            text-overflow: ellipsis;
            white-space: nowrap;
            font-family: 'Dancing Script', cursive;
        }
    </style>
    <link href="https://fonts.googleapis.com/css2?family=Dancing+Script&display=swap" rel="stylesheet">
</head>
<body>
    <h1>My Digital Bookshelf</h1>
    <div id="bookshelf"></div>
    <script>
        let books = JSON.parse(localStorage.getItem("books")) || [];

        function displayBooks() {
            const bookshelf = document.getElementById("bookshelf");
            bookshelf.innerHTML = "";
            books.forEach(book => {
                const bookDiv = document.createElement("div");
                bookDiv.classList.add("book");
                const bookLink = document.createElement("a");
                bookLink.href = book.pdfData;
                bookLink.download = book.title + ".pdf";
                const coverImg = document.createElement("img");
                coverImg.src = book.cover;
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
    </script>
</body>
</html>
---

