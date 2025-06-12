# Wanderlust - Your Ultimate Travel Blog 🌍✈️

WanderLust is a simple MERN travel blog website ✈ This project is aimed to help people to contribute in open source, upskill in react and also master git.

![Preview Image](https://github.com/krishnaacharyaa/wanderlust/assets/116620586/17ba9da6-225f-481d-87c0-5d5a010a9538)

## [Figma Design File](https://www.figma.com/file/zqNcWGGKBo5Q2TwwVgR6G5/WanderLust--A-Travel-Blog-App?type=design&node-id=0%3A1&mode=design&t=c4oCG8N1Fjf7pxTt-1)
## [Discord Channel](https://discord.gg/FEKasAdCrG)

## 🎯 Goal of this project

At its core, this project embodies two important aims:

1. **Start Your Open Source Journey**: It's aimed to kickstart your open-source journey. Here, you'll learn the basics of Git and get a solid grip on the MERN stack and I strongly believe that learning and building should go hand in hand.
2. **React Mastery**: Once you've got the basics down, a whole new adventure begins of mastering React. This project covers everything, from simple form validation to advanced performance enhancements. And I've planned much more cool stuff to add in the near future if the project hits more number of contributors.

_I'd love for you to make the most of this project - it's all about learning, helping, and growing in the open-source world._

## Setting up the project locally- Containerizing

1. Docker file for backend
   
                     FROM node:18-alpine

                     WORKDIR /app

                     COPY package*.json ./

                     RUN npm install

                     COPY . .

                     EXPOSE 5000

                     CMD ["npm","start"]
   
2. Docker file for frontend 

   ```bash
                    FROM node:18-alpine AS builder

                    WORKDIR /app

                    COPY package*.json ./

                    RUN npm install

                    COPY . .

                    FROM node:18-alpine

                    WORKDIR /app

                    COPY --from=builder /app ./

                    ENTRYPOINT ["npm", "run", "dev", "--", "--host"]
   ```

3. Docker-compose file

   ```bash

    version: "3.8"

        services:
    backend:
    container_name: backend
    build: ./backend
    ports:
      - "5000:5000"
    env_file:
      - ./backend/.env.sample
    depends_on:
      - mongo
   
    frontend:
    container_name: frontend
    build: ./frontend
    ports:
      - "5173:5173"
    depends_on:
      - backend
    env_file:
      - ./frontend/.env.local

   mongo:
    container_name: mongo
    image: mongo:latest
    ports:
      - "27017:27017"
    volumes:
      - ./backend/data:/data

   volumes:
   data:
   ```

4. **Configure Environment Variables-backend**
          #backend/.env.sample
      
         MONGODB_URI="mongodb://mongo/wanderlust"
         CORS_ORIGIN="http:localhost:5173"
7. **Configure Environment Variables-backend**
        # frontend/.env.local

         VITE_API_PATH="http://localhost:5000"

 6.  **Set up your MongoDB Database**

   ```bash
  - Open MongoDB Compass and connect MongoDB locally at `mongodb://localhost:27017`.
 
   ```
7.  **Import sample data**

   > To populate the database with sample posts, you can copy the content from the `backend/data/sample_posts.json` file and insert it as a document in the `wanderlust/posts` collection in your local MongoDB database using either MongoDB Compass or `mongoimport`.

   ```bash
   mongoimport --db wanderlust --collection posts --file ./data/sample_posts.json --jsonArray
   ```


### Issues



## 🌟 Ready to Contribute?

Kindly go through [CONTRIBUTING.md](https://github.com/krishnaacharyaa/wanderlust/blob/main/.github/CONTRIBUTING.md) to understand everything from setup to contributing guidelines.

## 💖 Show Your Support

If you find this project interesting and inspiring, please consider showing your support by starring it on GitHub! Your star goes a long way in helping me reach more developers and encourages me to keep enhancing the project.

🚀 Feel free to get in touch with me for any further queries or support, happy to help :)
