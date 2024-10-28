# CRUD Post Management Application

A JavaScript web application for managing user posts with CRUD (Create, Read, Update, Delete) functionality, using the TarmeezAcademy API.

## Features

- **Get Posts**: Fetches and displays posts for a specific user.
- **Create Post**: Allows users to add new posts with a title, body, and image.
- **Update Post**: Allows users to modify their existing posts.
- **Delete Post**: Allows users to delete their posts.

## Code Overview

### 1. Fetch and Display Posts

The `getposts` function fetches posts for a user, checks if the current user is the post author, and conditionally displays **Edit** and **Delete** buttons.

```javascript
function getposts() {
    const baseurl = "https://tarmeezAcademy.com/api/v1/";
    const urlparams = new URLSearchParams(window.location.search);
    const userId = urlparams.get("userid");

    axios.get(`${baseurl}users/${userId}/posts`)
        .then(function(response) {
            const posts = response.data.data;
            const user = getcurrentuser();
            const userId = user ? user.id : null;
            document.getElementById("user-posts").innerHTML = "";

            for (const post of posts) {
                const author = post.author;
                const isAuthor = userId && post.author.id === userId;

                let posttitle = post.title || "";
                const editButton = isAuthor ? `<button class='btn btn-secondary btn-sm' onclick="editpostbtnlicked('${encodeURIComponent(JSON.stringify(post))}')">Edit</button>` : '';
                const deleteButton = isAuthor ? `<button class='btn btn-danger btn-sm ms-2' onclick="deletepostbtnlicked('${encodeURIComponent(JSON.stringify(post))}')">Delete</button>` : '';

                let content = `
                <div class="card shadow">
                    <div class="card-header d-flex align-items-center justify-content-between">
                        <div class="d-flex align-items-center">
                            <img src="${author.profile_image}" alt="" style="width:40px; height:40px;" class="rounded-circle border border-2">
                            <b class="ms-2">${author.username}</b>
                        </div>
                        <div>${editButton} ${deleteButton}</div>
                    </div>
                    <div class="card-body" onclick="postclicked(${post.id})">
                        <img src="${post.image}" alt="Post image" class="w-100 mb-3">
                        <h6 class="text-muted">${post.created_at}</h6>
                        <h5 class="card-title">${posttitle}</h5>
                        <p class="card-text">${post.body}</p>
                        <div class="d-flex align-items-center">
                            <span>(${post.comments_count}) Comments</span>
                            <span id="post-tags-${post.id}" class="ms-2"></span>
                        </div>
                    </div>
                </div>`;

                document.getElementById("user-posts").innerHTML += content;
                const currentposttagID = `post-tags-${post.id}`;
                document.getElementById(currentposttagID).innerHTML = post.tags.map(tag => `<button class="btn btn-sm rounded-5" style="background-color: grey; color: white;">${tag.name}</button>`).join("");
            }
        })
        .catch(error => console.log(error));
}
