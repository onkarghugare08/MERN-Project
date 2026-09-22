FROM node:20-alpine

WORKDIR /app

# Install deps first for better layer caching
COPY package*.json ./
RUN npm install --omit=dev

# App source
COPY . .

# Persisted at runtime via volumes, but ensure they exist in the image too,
# then hand ownership to a non-root user before switching to it
RUN mkdir -p uploads pdfs \
    && addgroup -S app && adduser -S app -G app \
    && chown -R app:app /app

USER app

EXPOSE 5000

CMD ["node", "server.js"]