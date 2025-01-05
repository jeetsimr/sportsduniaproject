1. Overview
This is a simple project for searching news articles using the NewsAPI.
Users can search for news articles by entering a query, and the top three results will be displayed in
a user-friendly card format.
Additionally, if a user is not logged in, a popup will appear asking them to log in or sign up before
proceeding with the payment for premium articles.
If the user is logged in, they will be able to directly access the payment screen.
2. GitHub Repository Link
The project has been uploaded to GitHub for easy sharing and collaboration.
Here is the link to the GitHub repository:
https://github.com/yourusername/news-search-app
Replace 'yourusername' with your actual GitHub username to access the project.
3. Project Code
Below is the JavaScript code used to implement the news search feature, login/signup functionality,
and payment popup:
```javascript
const apiKey = 'f2a1cf1647534c3faaabc1af76f98952'; // Replace with your NewsAPI key
const searchInput = document.getElementById('search-input');
const searchResults = document.getElementById('search-results');
async function searchNews() {
 const query = searchInput.value;
 if (!query) return; // Avoid making request if search box is empty
 try {
 const response = await
fetch(`https://newsapi.org/v2/everything?q=${query}&sortBy=publishedAt&apiKey=${apiKey}`);
 const data = await response.json();
 
 if (data.articles.length > 0) {
 // Show search results in one card with topic name
 searchResults.innerHTML = `
 <div class="card">
 <h2>You searched for: ${query}</h2>
 ${data.articles.slice(0, 3).map((article, index) => `
 <p><strong>${article.title}</strong></p>
 <p>${article.description || 'No description available.'}</p>
 <p class="author">Author: ${article.author || 'Unknown'}</p>
 <p class="source">Source: ${article.source.name}</p>
 <p class="date">Published: ${new
Date(article.publishedAt).toLocaleDateString()}</p>
 <button class="read-more" onclick="window.open('${article.url}', '_blank')">Read
More</button>
 <hr>
 `).join('')}
 </div>
 `;
 } else {
 searchResults.innerHTML = '<p>No results found. Please try a different search.</p>';
 }
 } catch (error) {
 console.error('Error fetching search results:', error);
 searchResults.innerHTML = '<p>Error fetching news. Please try again later.</p>';
 }
}
```
This code handles user search, displays articles, and prompts the user for login/signup based on
their authentication status.
```html
<!DOCTYPE html>
<html lang="en">
<head>
 <meta charset="UTF-8">
 <meta name="viewport" content="width=device-width, initial-scale=1.0">
 <title>News Search App</title>
 <link rel="stylesheet" href="style.css">
</head>
<body>
 <div id="search-container">
 <input type="text" id="search-input" placeholder="Search for news...">
 <button onclick="searchNews()">Search</button>
 </div>
 <div id="search-results"></div>
 
 <!-- Login/Signup Popup -->
 <div id="login-popup" style="display:none;">
 <div class="popup-content">
 <span class="close-btn" onclick="closePopup()">X</span>
 <div id="login-form">
 <h2>Login</h2>
 <input type="text" id="username" placeholder="Username">
 <input type="password" id="password" placeholder="Password">
 <button onclick="handleLogin(event)">Login</button>
 <p>Don't have an account? <a href="javascript:void(0);" onclick="showSignup()">Sign
Up</a></p>
 </div>
 <div id="signup-form" style="display:none;">
 <h2>Sign Up</h2>
 <input type="text" id="new-username" placeholder="New Username">
 <input type="password" id="new-password" placeholder="New Password">
 <button onclick="handleSignup(event)">Sign Up</button>
 <p>Already have an account? <a href="javascript:void(0);"
onclick="showLogin()">Login</a></p>
 </div>
 </div>
 </div>
</body>
</html>
```
This is the structure of the app, including HTML and Java
