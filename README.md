# bespinterest
Application for sharing and managing images on a personal board

## Feature
* add board - user can add board to assign images to certain board
* add image - image will automatically assign under public board
* set board - users can assign image to board
* profile - user can set profile pictures and description

* follow - users can follow another users, it will show on profile page
* chat - users can chat with following each other user, multiple users can be in one chat room

## Demo
![bespin-demo2](https://user-images.githubusercontent.com/30321742/36122836-d2737c80-1018-11e8-9900-545c00d3327d.gif)

## Code Example

#### Handling board get request

```JS
board: {
  get: function(req, res) {
      let reqParams = url.parse(req.url, true).query;
      reqParams.boardId === '-1'
        ? db.Post
            .findAll()
            .then(function(data) {
              res.status(200).send(data);
            })
            .catch(function(err) {
              console.log(err);
              res.sendStatus(400);
            })
        : db.sequelize.query(`SELECT * FROM posts INNER JOIN boardposts ON boardposts."boardId" = ${reqParams.boardId} AND posts.id = boardposts."postId"`)
            .then(function(data) {
              res.status(200).send(data[0]);
            })
            .catch(function(err) {
              console.log(err);
              res.sendStatus(400);
            });
    }
  },

```
#### Fetching item associated with board

```JS
  handleFetchBoard(boardId) {
    axios
      .get('/board', {
        params: {
          boardId: boardId
        }
      })
      .then((res) => {
        this.setState({
          posts: res.data
        });
      })
      .catch((err) => console.log(err));
  }
```

## Running locally
before you run this app, you need to connect with postgresql

in terminal
```
1. npm install
2. npm run react-dev
3. npm start
```
now go to http://localhost:3000/

## Tech Stack
* Javascript
* React
* React Router
* PostgreSQL
* Sequelize
* Axios
* Express
* Node.js

## Authors
* Sohee Lim
* Samuel Kwak
* Yusaky Kasahara
* Jimmy Sandrs-Cannon

## License
This project is licensed under the MIT License
