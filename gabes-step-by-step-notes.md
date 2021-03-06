# Gabe's Steps to creating a server

1. `cd` to right folder
2. create new project folder
3. `cd` into new folder
4. `npx gitignore node`
5. initialize a git repo - `git init`
    ..* command line should now show the branch name
6. `npm init -y` (y keeps you from answering questions)
    ..* You should now have a package.json file
7. edit package.json
    ..*`"start": "node index.js"`
8. `npm i express`
9. touch `index.js`
10. `code .`
    ..* should see 4 files and 1 folder
11. in the index.js file add the following:
    ```const express= require('express)
    const PORT = process.env.PORT || 3300
    const server = express()
    server.use(express.json())

    server.get('/api', (req, res) => {
        res.json({ message: 'API is up!!!"})
    })

    server.listen(PORT, () => {
        console.log(`listening on` + PORT)
    })```
12. in terminal start server with `node index.js`
    ..* You should see `listening on 3300`
13. check endpoint
    `Get localhost:3300/api`
    ..* you should see `{"message: 'API is up'}`
14. in terminal `npx create-react-app client`
    ..* this will create a react app in a client folder inside the current git repo
15. in main index.js (while CRA is running) add the following after the server.use(express.json())
    ```//servering out static assets
    // ./client/build
    server.use(express.static(path.join(__dirname, 'client/build')))```

16. add the following after your first server.get
   ` // fallback endpoint that sends index.html
    server.get('*', (req, res) => {
        res.sendFile(path.join(__dirname, 'client/build', 'index.html'))
    })`
17. `cd client`
18. `npm run build` (this will create the build folder mentioned above) (this is how you would create a folder that you can upload to a hosting company to host your CRA)
19. `cd ..` and then `npm start` (just the server)
20. in browser you can now go to http://localhost:3300 and you should see the react app.
21. in main package.json (not client) add the following script
    `"postinstall": "cd client && npm i && npm run build"`
22. create a repo on github
    make sure it is public
    name it
    and click create
23. Grab the line in the add repo line
   ` git remote add origin <git link>`
    a. you can also do the following:
        `git remote set-url origin <git link>`
24. then push to git
25. deploy to heroku
    a. create new app
    b. find repo via github
    c. make sure it is the right branch
    d. click deploy (it will take longer this time)
26. when it is done view the app.

You should see the same thing you did locally
