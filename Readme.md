1. npm init -y
2. npm i express mongoose dotenv cors
3. npm install typescript --save-dev
4. tsc -init
5. tsconfig.json ->
   - search for "rootDir" change the path to "./src"
   - search for "outDir" change the path to "./dist"
6. Create 'src' folder inside of src:

   - create Files: 'app.ts' & 'server.ts'
   - create Folder: app -> config -> index.ts

7. Paste the bellow code at 'app.ts' and install required types :

   ```
   import express, { Application, Request, Response } from "express";
   import cors from "cors";
   const app: Application = express();
   const port = 3000;

    //PARSER
    app.use(express.json());
    app.use(cors());

    app.get("/", (req: Request, res: Response) => {
    res.send("Hello World!");
    });

    export default app;
   ```

   Types installation:

   - npm i --save-dev @types/express
   - npm i --save-dev @types/node
   - npm i --save-dev @types/cors

8. Paste the bellow code at 'server.ts':

   ```
    import mongoose from "mongoose";
    import config from "./app/config";
    import app from "./app";

    async function main() {
    try {
        await mongoose.connect(config.database_url as string);
        app.listen(config.port, () => {
        console.log(`Example app listening on port ${config.  port}`);
        });
    } catch (error) {
        console.log(error);
    }
    }

    main();
   ```

9. Paste the bellow code to the "src/app/config/index.ts" file:

   ```
   import dotenv from "dotenv";
   import path from "path";

   dotenv.config({ path: path.join((process.cwd(), ".env")) });

   export default {
       port: process.env.PORT,
       database_url: process.env.DATABASE_URL,
   };
   ```

10. Paste the bellow code to the '.env' :
    ```
    PORT=5000
    DATABASE_URL=mongodb+srv://<username>:<password>@cluster0.1llmf6a.mongodb.net/<DataBase_name>?retryWrites=true&w=majority&appName=Cluster0
    ```
    Replace the MongoDB URL:
    - Replace `<username>` & `<password>` to your actual username and password
    - Replace `<DataBase_name>` to your actual database name

### ESLINT setup:

- npm install eslint @typescript-eslint/parser @typescript-eslint/eslint-plugin --save-dev

- npx eslint --init

### Write start script for auto update

- npm i ts-node-dev --save-dev
- "start:dev": "ts-node-dev --respawn --transpile-only src/server.ts"
