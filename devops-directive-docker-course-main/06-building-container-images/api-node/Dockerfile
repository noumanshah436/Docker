FROM ubuntu

# RUN apt update
# RUN apt install nodejs -y

# try to combine commands
RUN apt update && apt install nodejs npm -y

# copy the entire current directory into the image
COPY . .

RUN npm install

CMD ["npm", "run", "dev"]
