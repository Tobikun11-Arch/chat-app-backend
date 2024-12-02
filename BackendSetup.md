1. npm init -y //generate package.json
2. npm install express@4.21.1 @types/express@4.17.17 //don't use latest it will not work
3. npm i -D typescript
4. npm i dotenv
5. npm i cors
6. npm i --save-dev @types/cors
7. create tsconfig.json file and put this 
{
    "compilerOptions": {
      "target": "ES6",
      "module": "commonjs",
      "strict": true,
      "esModuleInterop": true,
      "allowSyntheticDefaultImports": true,  
      "skipLibCheck": true,
      "outDir": "./dist"
    },
    "include": ["src/**/*.ts", "api/**/*.ts"],
    "exclude": ["node_modules"]
  }
8. in package.json in script part add this  "dev": "nodemon --watch \"api/**/*.ts\" --exec \"ts-node\" api/index.ts"
9. create folder named api then file index.ts --> api/index.ts
10. inside of index.ts paste this:
//api/index.ts
import dotenv from 'dotenv';
import cors from 'cors';
import express, { Request, Response } from 'express'
const app = express()
const port = 5000

dotenv.config();
const corsOptions = {
    origin: ['http://localhost:3000'],
    methods: ['GET', 'POST', 'PUT', 'DELETE', 'OPTIONS'],
    allowedHeaders: ['Content-Type', 'Authorization'],
    credentials: true 
};
app.use(cors(corsOptions));

app.get('/', (req: Request, res: Response) => {
  res.send('Hello World!')
})

app.get('/users/data', (req: Request, res: Response) => {
    const user = 'user'

    return res.json({ user })
})

app.listen(port, () => {
  console.log(`Example app listening on port ${port}`)
})

Last in terminal, 'npm run dev' to run remove ' '