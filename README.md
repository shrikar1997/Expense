const posts = [];
let lastActivityTime = null;

function createPost(post) {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            posts.push(post);
            resolve();
        }, 1000);
    });
}

function updateLastUserActivityTime() {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            lastActivityTime = new Date().toLocaleString();
            resolve();
        }, 1000);
    });
}

function deleteLastPost() {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            if (posts.length > 0) {
                const deletedPost = posts.pop();
                resolve(deletedPost);
            } else {
                reject("ERROR: NO POST FOUND");
            }
        }, 1000);
    });
}

createPost({ title: "Post 1" })
    .then(() => {
        return updateLastUserActivityTime();
    })
    .then(() => {
        return createPost({ title: "Post 2" });
    })
    .then(() => {
        return updateLastUserActivityTime();
    })
    .then(() => {
        console.log("Posts:", posts);
        console.log("Last Activity Time:", lastActivityTime);
        return deleteLastPost();
    })
    .then((deletedPost) => {
        console.log("Deleted Post:", deletedPost);
        console.log("Updated Posts:", posts);
    })
    .catch((error) => {
        console.log(error);
    });
