# JavaScript CRUD Operations

Welcome to the JavaScript CRUD Operations guide! This document provides a comprehensive overview of functions to create, read, update, and delete posts using JavaScript and Axios.

## Table of Contents
1. [getPosts](#getposts)
2. [editPostBtnClicked](#editpostbtnclicked)
3. [creatingPost](#creatingpost)
4. [deletePostBtnClicked](#deletepostbtnclicked)
5. [deletePost](#deletepost)

## JavaScript Functions

##getposts

```javascript
// Fetches posts for a specific user and displays them in the HTML.
function getPosts() {
    const baseurl = "https://tarmeezAcademy.com/api/v1/";
    const urlparams = new URLSearchParams(window.location.search);
    const userId = urlparams.get("userid");

    axios.get(`${baseurl}users/${userId}/posts`)
        .then(function(response) {
            const posts = response.data.data;
            const user = getCurrentUser(); // Get the current logged-in user
            const userId = user ? user.id : null; // Current user ID

            document.getElementById("user-posts").innerHTML = "";

            for (const post of posts) {
                const author = post.author;
                const isAuthor = userId && post.author.id === userId; // Check if the current user is the author

                let postTitle = post.title || "";

                // Conditional buttons for edit and delete
                const editButton = isAuthor ? `<button id="edit-btn" class='btn btn-secondary btn-sm' onclick="editPostBtnClicked('${encodeURIComponent(JSON.stringify(post))}')">Edit</button>` : '';
                const deleteButton = isAuthor ? `<button id="delete-btn" class='btn btn-danger btn-sm ms-2' onclick="deletePostBtnClicked('${encodeURIComponent(JSON.stringify(post))}')">Delete</button>` : '';

                let content = `
                <div class="card shadow">
                    <div class="card-header d-flex align-items-center justify-content-between">
                        <div class="d-flex align-items-center">
                            <img class="rounded-circle border border-2" src="${author.profile_image}" alt="" style="width:40px; height:40px;">
                            <b class="ms-2">${author.username}</b>
                        </div>
                        <div>
                            ${editButton}
                            ${deleteButton}
                        </div>
                    </div>
                    <div class="card-body" onclick="postClicked(${post.id})" style="cursor:pointer">
                        <img class="w-100 mb-3" src="${post.image}" alt="Post image">
                        <h6 class="text-muted">${post.created_at}</h6>
                        <h5 class="card-title">${postTitle}</h5>
                        <p class="card-text">${post.body}</p>
                        <hr>
                        <div class="d-flex align-items-center">
                            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-pen me-2" viewBox="0 0 16 16">
                                <path d="m13.498.795.149-.149a1.207 1.207 0 1 1 1.707 1.708l-.149.148a1.5 1.5 0 0 1-.059 2.059L4.854 14.854a.5.5 0 0 1-.233.131l-4 1a.5.5 0 0 1-.606-.606l1-4a.5.5 0 0 1 .131-.232l9.642-9.642a.5.5 0 0 0-.642.056L6.854 4.854a.5.5 0 1 1-.708-.708L9.44.854A1.5 1.5 0 0 1 11.5.796a1.5 1.5 0 0 1 1.998-.001m-.644.766a.5.5 0 0 0-.707 0L1.95 11.756l-.764 3.057 3.057-.764L14.44 3.854a.5.5 0 0 0 0-.708z"/>
                            </svg>
                            <span>(${post.comments_count}) Comments</span>
                            <span id="post-tags-${post.id}" class="ms-2"></span>
                        </div>
                    </div>
                </div>
                `;

                document.getElementById("user-posts").innerHTML += content;

                const currentPostTagID = `post-tags-${post.id}`;
                document.getElementById(currentPostTagID).innerHTML = "";

                for (const tag of post.tags) {
                    let contentTags = `<button class="btn btn-sm rounded-5" style="color: white; background-color: grey"> ${tag.name} </button>`;
                    document.getElementById(currentPostTagID).innerHTML += contentTags;
                }
            }
        })
        .catch(function(error) {
            console.log(error);
        });
}
```


##editpostbtnclicked

```javascript

// Handles the click event for editing a post.
function editPostBtnClicked(postObject) {
    const postIdInput = document.getElementById("post-id-input");
    const postId = postIdInput ? postIdInput.value.trim() : '';
  
    let post = JSON.parse(decodeURIComponent(postObject));
    console.log("clicked");
    console.log(post);
     
    document.getElementById("submit-post").innerHTML = "Update";
    document.getElementById("post-title-label").innerHTML = "Edit Post";
    document.getElementById("post-id-input").value = post.id;
    document.getElementById("post-address").value = post.title;
    document.getElementById("content-post").value = post.body;

    let modalPost = new bootstrap.Modal(document.getElementById("postmodal"), {});
    modalPost.toggle();
}
```

 Creates or updates a post based on whether the post ID is present.
```javascript

function creatingPost() {
    const baseurl = "https://tarmeezAcademy.com/api/v1"; // Ensure there's no trailing slash

    const postIdInput = document.getElementById("post-id-input");
    const postId = postIdInput ? postIdInput.value.trim() : '';
    const isCreate = !postId; // Determine if creating a new post

    const title = document.getElementById("post-address").value;
    const body = document.getElementById("content-post").value;
    const image = document.getElementById("image-post").files[0];
    const token = localStorage.getItem("token");

    let formData = new FormData();
    formData.append("body", body);
    formData.append("title", title);
    formData.append("image", image);

    const headers = {
        "Authorization": `Bearer ${token}`
    };

    if (isCreate) {
        let url = `${baseurl}/posts`; // Default URL for creating a new post
        // Creating a new post
        axios.post(url, formData, { headers: headers })
            .then((response) => {
                console.log("Post created successfully:", response.data); // Log response data
                const modal = document.getElementById("postmodal");
                const modalInstance = bootstrap.Modal.getInstance(modal);
                modalInstance.hide();
                showAlert("New Post Has Been Created", "success");
                getPosts();
            })
            .catch((error) => {
                const message = error.response?.data?.message || 'An error occurred';
                showAlert(message, "danger");
            });
    } else {
        formData.append("_method", "put");
        url = `${baseurl}/posts/${postId}`;
        
        axios.post(url, formData, {
            headers: headers
        })
        .then((response) => {
            const modal = document.getElementById("postmodal");
            const modalInstance = bootstrap.Modal.getInstance(modal);
            modalInstance.hide();
            showAlert("Post updated successfully", "success");
            getPosts();
        })
        .catch((error) => {
            const message = error.response.data.message;
            showAlert(message, "danger");
        });
    }
}

```
 Creates or updates a post based on whether the post ID is present.
```javascript

// Handles the click event for deleting a post.
function deletePostBtnClicked(postObjectDelete) {
    let post = JSON.parse(decodeURIComponent(postObjectDelete));
    console.log(post);
    document.getElementById("post-id-delete").value = post.id;

    let modalPost = new bootstrap.Modal(document.getElementById("deletemodal"), {});
    modalPost.toggle();
}

// Deletes a post after confirmation.
function deletePost() {
    const token = localStorage.getItem("token");
    if (!token) {
        console.error("Token not found. User might not be logged in.");
        showAlert("You're not authorized to delete this post. Please log in.", 'danger');
        return;
    }

    const postId = document.getElementById("post-id-delete").value;
    const url = `${baseurl}posts/${postId}`;

    const headers = {
        "Authorization": `Bearer ${token}`
    };

    axios.delete(url, { headers: headers })
        .then((response) => {
            console.log("Post deleted successfully:", response.data);
            const modal = document.getElementById("deletemodal");
            const modalInstance = bootstrap.Modal.getInstance(modal);
            modalInstance.hide();
            showAlert("Post deleted successfully", "success");
            getPosts();
        })
        .catch((error) => {
            const message = error.response?.data?.message || 'An error occurred';
            showAlert(message, "danger");
        });
}
