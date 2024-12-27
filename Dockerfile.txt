# Install dependencies
RUN npm install

# Copy the rest of the app's code
COPY . .

# Build the React app
RUN npm run build

# Step 2: Use an Nginx image to serve the React app
FROM nginx:alpine

# Copy the built React app to the Nginx HTML folder
COPY --from=builder /app/build /usr/share/nginx/html

# Expose port 80
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]