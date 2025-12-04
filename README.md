# Simple Blog

A minimal blog system built using HTML, CSS, JavaScript, PHP, and MySQL. It allows users to create posts, like posts, and leave comments (including replies).

## Features

- **Create Posts**: Easily publish new blog posts.
- **Like Posts**: Users can like posts by clicking a heart button.
- **Comments**: Readers can add comments to posts.
- **Replies to Comments**: Users can reply to comments, and replies from the author are highlighted with a special badge.

## Requirements

- **XAMPP** (for Apache and MySQL)
- A web browser (e.g., Chrome, Firefox)

## Setup Instructions

### 1. Start XAMPP

- Open **XAMPP Control Panel** and start the following services:
  - **Apache**
  - **MySQL**

### 2. Create the Database

- Go to **http://localhost/phpmyadmin** in your browser.
- Click on the **SQL** tab.
- Paste the contents of `database.sql` (or the SQL script provided below) into the query box and run it.

Alternatively, you can use the following SQL code directly:

```sql
CREATE DATABASE IF NOT EXISTS simple_blog;
USE simple_blog;

CREATE TABLE IF NOT EXISTS posts (
    id INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    content TEXT NOT NULL,
    author VARCHAR(100) NOT NULL,
    image VARCHAR(255),
    like_count INT DEFAULT 0,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE IF NOT EXISTS comments (
    id INT AUTO_INCREMENT PRIMARY KEY,
    post_id INT NOT NULL,
    author VARCHAR(100) NOT NULL,
    comment TEXT NOT NULL,
    parent_id INT DEFAULT NULL,
    is_author BOOLEAN DEFAULT FALSE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (post_id) REFERENCES posts(id) ON DELETE CASCADE,
    FOREIGN KEY (parent_id) REFERENCES comments(id) ON DELETE CASCADE
);
```

3. Access the Site

Open your browser and go to http://localhost/web_proj/
 to access the blog.

How to Use

Create a Post: Go to the "New Post" page in the navigation menu, fill in the form, and click Publish to post.

Like a Post: Click the heart icon on any post to like it.

Add a Comment: Scroll down on any post to the comment section and add your comment.

Reply to Comments: Click the "Reply" button under any comment. If you use the same name as the post author, you'll get an "Author" badge next to your reply.

File Structure

index.html: Homepage showing the list of posts.

new-post.html: Page for creating new blog posts.

post.html: Page for viewing individual posts and their comments.

css/style.css: Styles for the blog.

config/db.php: Database connection settings.

api/: Folder containing PHP files to handle the backend logic (e.g., fetching posts, submitting comments, etc.).

Database Configuration

If your MySQL setup uses different credentials (e.g., a password), you need to update the config/db.php file with the correct details:

$host = 'localhost';
$dbname = 'simple_blog';
$username = 'root';
$password = ''; // Add your password here if necessary

Troubleshooting

Can't connect to the database?

Ensure MySQL is running in XAMPP.

Verify that your credentials in config/db.php are correct.

Pages are not loading?

Make sure Apache is running.

Check that the project files are in the correct folder:
c:\xampp\htdocs\vachan_proj\web_proj\

Replies not working?

If you created the database before the reply feature was added, run update_database.sql to update the schema.

