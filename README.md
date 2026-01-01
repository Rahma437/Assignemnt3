// const fs = require("fs");

// const readStream = fs.createReadStream("./big.txt", {
//   encoding: "utf8",
//   highWaterMark: 1024,
// });

// readStream.on("data", (chunk) => {
//   console.log("Chunk received:");
//   console.log(chunk);
// });

// readStream.on("end", () => {
//   console.log("Finished reading file");
// });


// const fs = require("fs");

// const readStream = fs.createReadStream("./source.txt");
// const writeStream = fs.createWriteStream("./dest.txt");

// readStream.pipe(writeStream);

// writeStream.on("finish", () => {
//   console.log("File copied using streams");
// });



// const fs = require("fs");
// const zlib = require("zlib");

// const readStream = fs.createReadStream("./data.txt");
// const gzip = zlib.createGzip();
// const writeStream = fs.createWriteStream("./data.txt.gz");

// readStream.pipe(gzip).pipe(writeStream);

// writeStream.on("finish", () => {
//   console.log("File compressed successfully");
// });



// const http = require("http");
// const fs = require("fs");
// const url = require("url");

// const PORT = 3000;

// function getUsers() {
//   return JSON.parse(fs.readFileSync("./users.json", "utf8"));
// }

// function saveUsers(users) {
//   fs.writeFileSync("./users.json", JSON.stringify(users, null, 2));
// }

// const server = http.createServer((req, res) => {
//   const parsedUrl = url.parse(req.url, true);
//   const method = req.method;

//   // ADD USER
//   if (method === "POST" && parsedUrl.pathname === "/user") {
//     let body = "";
//     req.on("data", chunk => body += chunk);
//     req.on("end", () => {
//       const users = getUsers();
//       const newUser = JSON.parse(body);

//       const exists = users.find(u => u.email === newUser.email);
//       if (exists) {
//         res.end(JSON.stringify({ message: "Email already exists." }));
//         return;
//       }

//       newUser.id = users.length + 1;
//       users.push(newUser);
//       saveUsers(users);

//       res.end(JSON.stringify({ message: "User added successfully." }));
//     });
//   }

//   // UPDATE USER
//   else if (method === "PATCH" && parsedUrl.pathname.startsWith("/user/")) {
//     const id = parseInt(parsedUrl.pathname.split("/")[2]);
//     let body = "";

//     req.on("data", chunk => body += chunk);
//     req.on("end", () => {
//       const users = getUsers();
//       const user = users.find(u => u.id === id);

//       if (!user) {
//         res.end(JSON.stringify({ message: "User ID not found." }));
//         return;
//       }

//       Object.assign(user, JSON.parse(body));
//       saveUsers(users);

//       res.end(JSON.stringify({ message: "User updated successfully." }));
//     });
//   }

//   // DELETE USER
//   else if (method === "DELETE" && parsedUrl.pathname.startsWith("/user/")) {
//     const id = parseInt(parsedUrl.pathname.split("/")[2]);
//     let users = getUsers();

//     const index = users.findIndex(u => u.id === id);
//     if (index === -1) {
//       res.end(JSON.stringify({ message: "User ID not found." }));
//       return;
//     }

//     users.splice(index, 1);
//     saveUsers(users);

//     res.end(JSON.stringify({ message: "User deleted successfully." }));
//   }

//   // GET ALL USERS
//   else if (method === "GET" && parsedUrl.pathname === "/user") {
//     res.end(JSON.stringify(getUsers()));
//   }

//   // GET USER BY ID
//   else if (method === "GET" && parsedUrl.pathname.startsWith("/user/")) {
//     const id = parseInt(parsedUrl.pathname.split("/")[2]);
//     const users = getUsers();
//     const user = users.find(u => u.id === id);

//     if (!user) {
//       res.end(JSON.stringify({ message: "User not found." }));
//       return;
//     }

//     res.end(JSON.stringify(user));
//   }

//   else {
//     res.end("Route not found");
//   }
// });

// server.listen(PORT, () => {
//   console.log(`Server running on port ${PORT}`);
// });



//Event loop 
//asynchronous  Node.js   main thread  


//Event loop  Thread pool  Async 1/0


//Event loop  Callbacks Queue Thread pool   (crypto, fs)


//Call stack Event loop Event Queue  


//UV_THREADPOOL_SIZE=4

//Blocking   non-Blocking



