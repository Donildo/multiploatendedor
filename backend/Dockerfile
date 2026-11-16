FROM node:16-bullseye-slim

WORKDIR /app

RUN apt-get clean && rm -rf /var/lib/apt/lists/* \
  && apt-get update -o Acquire::Check-Valid-Until=false -o Acquire::Check-Date=false \
  && apt-get install -y --no-install-recommends \
    git wget curl ca-certificates \
    ffmpeg \
    chromium \
    fonts-liberation fonts-noto-color-emoji \
    libxss1 libnss3 libatk1.0-0 libatk-bridge2.0-0 libcups2 libdrm2 libxkbcommon0 \
    libxcomposite1 libxdamage1 libxfixes3 libxrandr2 libgbm1 libasound2 libgtk-3-0 \
  && rm -rf /var/lib/apt/lists/* \
  && npm install -g pm2

ENV PUPPETEER_SKIP_CHROMIUM_DOWNLOAD=true
ENV PUPPETEER_EXECUTABLE_PATH=/usr/bin/chromium
ENV CHROME_BIN=/usr/bin/chromium
ENV NODE_ENV=development

COPY package*.json ./
RUN npm install --legacy-peer-deps

COPY . .
RUN npm run build

EXPOSE 3000 3100
ENTRYPOINT ["npm", "run", "dev:server"]
