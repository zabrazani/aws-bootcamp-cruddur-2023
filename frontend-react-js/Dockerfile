# --- ADD THIS LINE (The Missing Base Image) ---
FROM node:18-alpine 
# ---------------------------------------------

COPY . /frontend-react-js
WORKDIR /frontend-react-js
RUN npm install
EXPOSE ${PORT}
CMD ["npm", "start"]